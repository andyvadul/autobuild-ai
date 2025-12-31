# Assignment: WP-004 - URGENT

**From:** lead_agent (manual assignment by human)
**To:** devops_agent
**Date:** 2025-12-03T01:45:00Z
**Priority:** CRITICAL
**Estimated Time:** 10-15 minutes

---

## Task Summary

Fix the broken `.github/workflows/plugin-check.yml` workflow that is failing on every commit.

## Context

The build is currently **RED** on master branch. Every push fails the Plugin Check workflow because of this error:

```
##[error]Can't find 'action.yml', 'action.yaml' or 'Dockerfile' for action 'WordPress/WordPress@master'.
```

This is **blocking all other agent work** because:
- Lead agent's build health checks will fail
- Dev agent's build verification will fail
- Cannot merge any PRs with failing status checks

## Your Task

1. **READ** `.claude/progress/URGENT-WP-004.md` for complete details
2. **CHOOSE** Option 1 (recommended) - remove the broken step
3. **EDIT** `.github/workflows/plugin-check.yml` (lines 36-40)
4. **TEST** if possible (optional if act not installed)
5. **CREATE** PR with fix
6. **UPDATE** features.json when complete

## Expected Output

- Feature branch: `fix/wp-004-plugin-check-workflow`
- PR created with clear description
- Workflow runs and passes (or at least doesn't fail with action not found)
- Status message in `.claude/progress/messages/devops-to-lead.md`

## Success Criteria

- [ ] Workflow file modified
- [ ] PR created
- [ ] Workflow runs without "action not found" error
- [ ] Build status improves (red → yellow or green)

---

**START THIS IMMEDIATELY - This is blocking everyone else.**

Please acknowledge by updating features.json status to "in_progress" when you begin.
