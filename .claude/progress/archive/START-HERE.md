# Quick Start - Fix WP-004 Then Launch Agents

**Status:** WP-004 URGENT assignment ready ✅
**Mode:** Normal (20-min sessions)
**Next:** Launch DevOps agent solo to fix build

---

## Step 1: Push the urgent assignment (if not done already)

```bash
cd /home/searchwiz/gitrepo/search_wiz
git push origin master
```

If git auth fails, that's OK - DevOps agent will push its own PR.

---

## Step 2: Launch DevOps Agent SOLO (20 min)

```bash
# Start DevOps in standalone session
tmux new -s devops-urgent
claude --model haiku
```

**First message to agent:**
```
Read .claude/agents/devops_agent.md and .claude/progress/URGENT-WP-004.md

Fix the broken plugin-check workflow immediately. Use Option 1: remove lines 36-40 from .github/workflows/plugin-check.yml
```

Wait 20 minutes for agent to create PR.

---

## Step 3: Review & Merge DevOps PR (5 min)

```bash
# Detach from tmux: Ctrl+B then d

# Check PR
gh pr list

# Merge it
gh pr merge <number> --squash --delete-branch

# Verify build is green
gh run list --limit 1
```

---

## Step 4: Launch All Agents (Normal Mode)

```bash
./scripts/agent-launch.sh
```

This creates 4 panes. Start agents in each pane:

**Lead (bottom-left):** `claude --model opus` → `Read .claude/agents/lead_agent.md and begin orchestration`

**Dev (top-left):** `claude --model sonnet` → `Read .claude/agents/dev_agent.md and start working`

**Test (top-right):** `claude --model haiku` → `Read .claude/agents/test_agent.md and start working`

**DevOps (bottom-right):** `claude --model haiku` → `Read .claude/agents/devops_agent.md and start working`

---

## What Happens Next (20 min each)

- **Lead:** Assigns WP-001 to Dev, TEST-007 to Test, WP-002 to DevOps
- **Dev:** Partial progress on WP-001 (2-3 of 5 files fixed)
- **Test:** Partial progress on TEST-007 (3-5 test stubs written)
- **DevOps:** Completes WP-002 or WP-003 fully

Expect PARTIAL work in 20-min sessions. That's normal.

---

## Files Created

✅ [URGENT-WP-004.md](.claude/progress/URGENT-WP-004.md) - Detailed instructions for DevOps
✅ [lead-to-devops.md](.claude/progress/messages/lead-to-devops.md) - Assignment message
✅ [features.json](.claude/progress/features.json) - WP-004 marked URGENT

**Everything is ready. Start with Step 2.**
