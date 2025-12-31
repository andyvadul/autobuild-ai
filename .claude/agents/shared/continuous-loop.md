# Continuous Work Loop Protocol

**All agents MUST follow this protocol for continuous operation.**

---

## Core Principle

**NEVER exit after completing a task.** Always check for more work.

```
┌─────────────────────────────────────────┐
│           CONTINUOUS LOOP               │
├─────────────────────────────────────────┤
│  1. Check queue for highest priority    │
│  2. If task found → work on it          │
│  3. Complete task → go to step 1        │
│  4. If no tasks → sleep 5 min           │
│  5. Wake up → go to step 1              │
│  6. If token limit → wait → resume      │
└─────────────────────────────────────────┘
```

---

## Work Loop Implementation

After your startup sequence, enter this loop:

```bash
work_loop() {
  while true; do
    echo ""
    echo "=== Checking for work: $(date) ==="

    # Pull latest changes
    git pull origin master 2>/dev/null || true

    # Check for blockers first
    if ls .claude/progress/notifications/BLOCKER-*.md 2>/dev/null | grep -q .; then
      echo "🚨 Blocker detected - waiting for resolution..."
      sleep 300  # 5 minutes
      continue
    fi

    # Select highest priority task
    TASK=$(select_work)

    if [ -n "$TASK" ]; then
      echo "📋 Found task: #$TASK"
      claim_task "$TASK"
      # ... do the work ...
      complete_task "$TASK"
      echo "✅ Task #$TASK completed"
      echo "🔄 Checking for next task..."
      # Loop continues - check for more work
    else
      echo "📭 No tasks available"
      echo "💤 Sleeping for 5 minutes..."
      sleep 300
      echo "⏰ Waking up - checking again..."
      # Loop continues
    fi
  done
}
```

---

## Token Limit Handling

When you hit a token/rate limit:

1. **Detect the limit** - Look for messages like:
   - "rate limit exceeded"
   - "token limit reached"
   - "quota exceeded"
   - "billing limit"

2. **Calculate wait time** - Usually shown in error message

3. **Wait and resume** - Don't exit, just pause

```bash
handle_token_limit() {
  WAIT_SECONDS=$1
  echo "⚠️ Token limit reached"
  echo "⏳ Waiting $WAIT_SECONDS seconds for quota reset..."
  sleep $WAIT_SECONDS
  echo "🔄 Resuming work loop..."
}
```

If no wait time specified, default to 60 seconds.

---

## Blocker Notification (Alert Lead Agent)

When you hit a blocker, **notify the lead agent via tmux** so they can investigate:

```bash
notify_lead_blocker() {
  BLOCKER_TYPE=$1
  BLOCKER_DETAILS=$2
  AGENT_NAME=$3

  # Send message to lead agent's tmux window
  tmux send-keys -t "searchwiz-agents:lead" \
    "🚨 BLOCKER from ${AGENT_NAME}_agent: ${BLOCKER_TYPE} - ${BLOCKER_DETAILS}. Please investigate." Enter 2>/dev/null || true

  # Also create a blocker file for persistence
  BLOCKER_FILE=".claude/progress/notifications/BLOCKER-${AGENT_NAME}-$(date +%Y%m%d%H%M%S).md"
  mkdir -p .claude/progress/notifications
  cat > "$BLOCKER_FILE" << EOF
# Blocker Alert

**Agent:** ${AGENT_NAME}_agent
**Time:** $(date -Iseconds)
**Type:** ${BLOCKER_TYPE}

## Details
${BLOCKER_DETAILS}

## Status
- [ ] Lead agent notified
- [ ] Investigation started
- [ ] Resolved
EOF

  echo "📢 Lead agent notified via tmux"
}
```

### When to Notify Lead

Notify the lead agent for:

| Blocker Type | Example | Action |
|--------------|---------|--------|
| `CI_FAILURE` | Build failing, not my code | `notify_lead_blocker "CI_FAILURE" "Tests failing on master - last commit by dev_agent" "$AGENT_NAME"` |
| `BILLING_LIMIT` | GitHub Actions quota exceeded | `notify_lead_blocker "BILLING_LIMIT" "GitHub Actions minutes exhausted" "$AGENT_NAME"` |
| `MISSING_SECRETS` | Deployment secrets not configured | `notify_lead_blocker "MISSING_SECRETS" "DREAMHOST_SSH_KEY not found" "$AGENT_NAME"` |
| `DEPENDENCY_BLOCKED` | Waiting on another agent | `notify_lead_blocker "DEPENDENCY_BLOCKED" "Issue #123 blocked by #120 (dev_agent)" "$AGENT_NAME"` |
| `PERMISSION_ERROR` | Can't access required resource | `notify_lead_blocker "PERMISSION_ERROR" "Cannot push to master branch" "$AGENT_NAME"` |

### Do NOT Notify Lead For

- No tasks available (just sleep)
- Token limits (just wait and resume)
- Normal task completion
- Expected test failures during TDD

---

## Priority-Based Work Selection

Always select work in this order:

```bash
select_work() {
  local AGENT_LABEL="agent:$AGENT_NAME"

  # Priority 1: Critical
  TASK=$(gh issue list --label "$AGENT_LABEL" --label "priority:critical" --label "status:pending" --json number --jq '.[0].number' 2>/dev/null)

  # Priority 2: High
  [ -z "$TASK" ] && TASK=$(gh issue list --label "$AGENT_LABEL" --label "priority:high" --label "status:pending" --json number --jq '.[0].number' 2>/dev/null)

  # Priority 3: Medium
  [ -z "$TASK" ] && TASK=$(gh issue list --label "$AGENT_LABEL" --label "priority:medium" --label "status:pending" --json number --jq '.[0].number' 2>/dev/null)

  # Priority 4: Any pending
  [ -z "$TASK" ] && TASK=$(gh issue list --label "$AGENT_LABEL" --label "status:pending" --json number --jq '.[0].number' 2>/dev/null)

  echo "$TASK"
}
```

---

## After Task Completion

**DO NOT:**
- Exit the process
- Wait for new instructions
- Ask what to do next

**DO:**
- Mark task complete
- Immediately check for next task
- Report status briefly

```bash
complete_task() {
  TASK=$1

  # Update GitHub
  gh issue edit "$TASK" \
    --remove-label "status:in-progress" \
    --add-label "status:complete"

  gh issue comment "$TASK" --body "✅ **Completed by ${AGENT_NAME}_agent**
Finished: $(date -Iseconds)
Checking for next task..."

  # Don't exit - let the loop continue
}
```

---

## Sleep Behavior

Only sleep when:
1. **No tasks available** - Sleep 5 minutes, then check again
2. **Token/rate limited** - Wait for quota reset, then resume
3. **Blocker detected** - Wait for devops/lead to resolve

Never sleep:
- After completing a task (check for more work immediately)
- When there are pending tasks in queue
- When told to work on something

---

## Example Full Loop

```bash
#!/bin/bash
AGENT_NAME="dev"

# Startup
echo "=== ${AGENT_NAME}_agent starting ==="
verify_environment

# Enter continuous loop
while true; do
  TASK=$(select_work)

  if [ -n "$TASK" ]; then
    claim_task "$TASK"

    # Do the actual work (this is where Claude does the task)
    # work_on_task "$TASK"

    complete_task "$TASK"

    # IMMEDIATELY check for more work
    continue
  else
    echo "No work found - sleeping 5 min"
    sleep 300
  fi
done
```

---

## Status Reporting

Every 30 minutes of work, output a brief status:

```
=== Agent Status ===
Agent: dev_agent
Uptime: 2h 15m
Tasks completed this session: 5
Current task: #142
Queue depth: 3 pending tasks
```

This helps monitoring without interrupting work.
