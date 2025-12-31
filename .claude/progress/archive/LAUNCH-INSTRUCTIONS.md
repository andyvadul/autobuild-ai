# Launch Instructions - Normal Mode with URGENT WP-004

**Created:** 2025-12-03T01:45:00Z
**Mode:** Normal (20-min sessions)
**Priority:** Fix WP-004 FIRST, then launch all agents

---

## Current Status

✅ **Assignment Created:**
- WP-004 marked as URGENT in features.json
- URGENT-WP-004.md created with detailed instructions
- lead-to-devops.md created with assignment message
- All files committed locally (need to push when you have git auth)

⚠️ **Build Status:**
- GitHub Actions: ❌ Plugin Check failing (WP-004)
- GitHub Actions: ⚠️ Lint warnings (not blocking)
- Local tests: ✅ Should pass (npm test, composer test)

---

## Step 1: Push Urgent Assignment (Manual)

You need to push the local commit since git auth failed in WSL:

```bash
# Option A: Push from your main machine (if you have git configured there)
cd /path/to/search_wiz
git pull origin master  # Get the local commit from WSL
git push origin master

# Option B: Configure git in WSL first
git config --global user.name "Andy Vadul"
git config --global user.email "andy@searchwiz.ai"
git push origin master
```

---

## Step 2: Launch DevOps Agent FIRST (Solo - 20 minutes)

**Why first?** WP-004 is blocking the build. Fix it before other agents start.

```bash
# In WSL or your dev machine
cd /home/searchwiz/gitrepo/search_wiz

# Launch tmux for DevOps agent
tmux new -s devops-urgent

# Inside tmux, start Claude CLI
claude --model haiku

# First message to DevOps agent:
```

**Copy/paste this to DevOps agent:**
```
Read .claude/agents/devops_agent.md and start working.

URGENT TASK ASSIGNED: Read .claude/progress/URGENT-WP-004.md and fix the broken plugin-check workflow immediately.

This is CRITICAL and blocking all builds. Follow Option 1 (fastest) - remove the broken WordPress/WordPress@master action from .github/workflows/plugin-check.yml lines 36-40.

After you create the PR, update features.json to mark WP-004 as "review" status.
```

---

## Step 3: Monitor DevOps Agent (0-20 minutes)

Watch the DevOps agent work:

**Expected timeline:**
- Min 0-2: Reads devops_agent.md and URGENT-WP-004.md
- Min 2-5: Reads .github/workflows/plugin-check.yml
- Min 5-8: Edits file to remove broken action
- Min 8-12: Creates feature branch, commits changes
- Min 12-15: Creates PR with gh pr create
- Min 15-18: Updates features.json, writes completion message
- Min 18-20: Exits cleanly

**What you should see:**
```bash
# DevOps agent will run commands like:
git checkout -b fix/wp-004-plugin-check-workflow
# ... edits plugin-check.yml ...
git add .github/workflows/plugin-check.yml
git commit -m "fix(ci): Remove broken WordPress/WordPress@master action"
git push origin fix/wp-004-plugin-check-workflow
gh pr create --title "fix(ci): Fix plugin-check workflow syntax error" --body "..."
```

---

## Step 4: Review and Merge DevOps PR (Manual - 5 minutes)

After DevOps agent finishes:

```bash
# Detach from tmux (Ctrl+B then d)

# Check PR was created
gh pr list

# Review the PR
gh pr view <PR_NUMBER> --web
# OR
gh pr diff <PR_NUMBER>

# If it looks good, merge it
gh pr merge <PR_NUMBER> --squash --delete-branch

# Verify build is now green (or at least not failing on action syntax)
gh run list --limit 1
```

---

## Step 5: Launch All Agents in Normal Mode (After WP-004 merged)

Once build is green:

```bash
# Launch all 4 agents in tmux
./scripts/agent-launch.sh

# This creates 4 panes:
# ┌─────────────────┬─────────────────┐
# │   Dev Agent     │   Test Agent    │
# │   (Sonnet)      │   (Haiku)       │
# ├─────────────────┼─────────────────┤
# │   Lead Agent    │  DevOps Agent   │
# │   (Opus)        │   (Haiku)       │
# └─────────────────┴─────────────────┘
```

**Start agents in this order:**

**Pane 1 (Lead Agent - bottom left):**
```
claude --model opus
> "Read .claude/agents/lead_agent.md and begin orchestration"
```

**Wait 2-3 minutes for Lead to assess state, then:**

**Pane 2 (Dev Agent - top left):**
```
claude --model sonnet
> "Read .claude/agents/dev_agent.md and start working"
```

**Pane 3 (Test Agent - top right):**
```
claude --model haiku
> "Read .claude/agents/test_agent.md and start working"
```

**Pane 4 (DevOps Agent - bottom right):**
```
claude --model haiku
> "Read .claude/agents/devops_agent.md and start working"
```

---

## What to Expect After 20 Minutes (Normal Mode)

### Lead Agent (Opus - 40 min session, but check at 20 min):
- ✅ Reads features.json, progress.md
- ✅ Checks build health (should be green now)
- ✅ Assigns WP-001 to dev_agent (post type migration)
- ✅ Assigns WP-002 or WP-003 to devops_agent (no conflict with dev work)
- ✅ Assigns TEST-007 to test_agent (functional tests)
- ✅ Updates features.json with assignments
- ✅ Creates assignment messages in .claude/progress/messages/

### Dev Agent (Sonnet - 20 min):
**If assigned WP-001:**
- ⚠️ PARTIAL completion (2-3 of 5 files fixed)
- ✅ Commits to feature branch
- ✅ Updates progress.md
- Status: "in_progress" (not complete)

**If no assignment yet:**
- ✅ Self-assigns TEST-001 (first unit test)
- ⚠️ PARTIAL completion (5-10 test methods written)
- ✅ Commits work
- Coverage: +3-5%

### Test Agent (Haiku - 20 min):
**If assigned TEST-007:**
- ✅ Reads 1-2 TESTING*.md files
- ✅ Counts scenarios (~70 total)
- ⚠️ PARTIAL completion (3-5 functional test stubs written)
- ✅ Updates progress.md with coverage table
- Functional coverage: 4-7% (3-5 of 70 scenarios)

**If no assignment:**
- ✅ Self-assigns DOC-002 (end-user docs)
- ⚠️ PARTIAL completion (getting-started.md written)
- ✅ Commits to feature branch

### DevOps Agent (Haiku - 20 min):
**If assigned WP-002 (create public repo):**
- ✅ COMPLETE - runs `gh repo create`
- ✅ Populates initial files
- ✅ Pushes to new repo
- ✅ Creates completion message

**If assigned WP-003 (move jest.setup.js):**
- ✅ COMPLETE - moves file
- ✅ Updates jest.config.js
- ✅ Creates PR

---

## Expected Git Status After 20 Minutes

```
On branch master
Changes committed locally:
  - .claude/progress/features.json (updated by all agents - might conflict!)
  - .claude/progress/progress.md (updated by all agents - might conflict!)

Feature branches created:
  - fix/wp-001-post-type-migration (dev_agent, partial)
  - feature/TEST-001-index-manager-tests (dev_agent, if self-assigned)
  - feature/TEST-007-functional-tests (test_agent, partial)
  - feature/DOC-002-user-docs (test_agent, if self-assigned)
  - feature/WP-002-public-repo (devops_agent, complete)

PRs created:
  - 0-1 PRs (only if devops_agent completed WP-002 or WP-003)
```

**Potential merge conflicts:**
- ⚠️ features.json (all agents update simultaneously)
- ⚠️ progress.md (all agents log simultaneously)

**How to resolve:**
```bash
# After 20 minutes, merge all progress files manually
git fetch origin
git pull origin master --rebase
# Resolve conflicts in features.json and progress.md
git add .claude/progress/
git rebase --continue
git push origin master
```

---

## Success Criteria - First 20-Minute Round

- ✅ WP-004 PR merged, build is green
- ✅ Lead agent assigned work to 3 workers
- ✅ Dev agent made progress on WP-001 or TEST-001 (partial)
- ✅ Test agent made progress on TEST-007 or DOC-002 (partial)
- ✅ DevOps agent completed WP-002 or WP-003 (full)
- ✅ No agents stuck or blocked
- ✅ All agents updated features.json (even if conflicted)
- ⚠️ Expect partial work, not completion

---

## Next Steps After First Round

### If Smooth:
1. Let agents continue for 2-3 more rounds (40-60 min total)
2. Monitor progress every 20 minutes
3. Merge any PRs that are created
4. Resolve any conflicts in progress files

### If Issues:
1. Stop agents: `tmux kill-session -t searchwiz-agents`
2. Review what went wrong
3. Fix blockers
4. Restart with corrected instructions

### If You Want Faster Progress:
1. Switch to aggressive mode (60-min sessions):
   ```bash
   ./scripts/agent-launch.sh --dev_aggressive --test_aggressive
   ```
2. Monitor every 60 minutes instead of 20
3. Expect COMPLETE work instead of partial

---

## Monitoring Commands

```bash
# Watch agent progress
tail -f .claude/progress/progress.md

# Check feature status
cat .claude/progress/features.json | jq '.features[] | select(.status=="in_progress")'

# Check for urgent items
ls .claude/progress/URGENT-*.md

# Check for blockers
ls .claude/progress/BLOCKER-*.md

# See recent commits
git log --oneline --graph --all | head -20

# Check PRs
gh pr list

# Check build status
gh run list --limit 3
```

---

## Emergency Stop

If something goes wrong:

```bash
# Kill all agents immediately
tmux kill-session -t searchwiz-agents

# Review last hour of work
git log --since="1 hour ago" --all --oneline --stat

# Rollback if needed
git reset --hard HEAD~5  # Roll back 5 commits
git push origin master --force  # CAREFUL!

# Or just revert specific commit
git revert <commit-hash>
```

---

**Ready to launch!** Start with Step 1 (push urgent assignment) then Step 2 (launch DevOps agent solo).
