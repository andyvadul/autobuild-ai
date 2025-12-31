# URGENT: Fix Broken GitHub Action Workflow

**Task:** WP-004
**Assigned:** devops_agent
**Priority:** CRITICAL
**Status:** BLOCKING ALL BUILDS
**Created:** 2025-12-03T01:45:00Z

---

## Problem Statement

The `.github/workflows/plugin-check.yml` workflow is **failing on every commit** due to a syntax error.

### Error Details

**File:** `.github/workflows/plugin-check.yml`
**Line:** 37-39
**Error:**
```
##[error]Can't find 'action.yml', 'action.yaml' or 'Dockerfile' for action 'WordPress/WordPress@master'.
```

**Root Cause:**
```yaml
- name: Setup WordPress
  uses: WordPress/WordPress@master  # ❌ This action does NOT exist in GitHub Actions
  id: setup-wp
  continue-on-error: true
```

The action `WordPress/WordPress@master` does not exist in the GitHub Actions marketplace.

### Impact

- ❌ Every push to master fails the Plugin Check workflow
- ❌ PRs show failing status checks
- ⚠️ Blocks agent work because build health checks will fail
- ⚠️ Blocks WordPress.org submission workflow

### Evidence

```bash
# Recent failed runs:
gh run list --limit 5
# Output shows:
# completed  failure  WordPress Plugin Check  master  push  19879436280
# completed  failure  WordPress Plugin Check  master  push  19879168936
```

---

## Solution Options

### Option 1: Remove the Broken Step (RECOMMENDED - Fastest)

**Edit `.github/workflows/plugin-check.yml`:**
```yaml
# DELETE or COMMENT OUT lines 36-40:
# - name: Setup WordPress
#   uses: WordPress/WordPress@master
#   id: setup-wp
#   continue-on-error: true
```

**Why this works:**
- The step isn't actually used in subsequent steps
- The workflow currently only validates plugin structure, not WordPress integration
- Can be properly implemented later when needed

**Time:** 5 minutes

---

### Option 2: Use Proper WordPress Plugin Check Action

**Replace lines 36-110 with:**
```yaml
- name: WordPress Plugin Check
  uses: swissspidy/wp-plugin-check-action@v1
  with:
    repo-token: '${{ secrets.GITHUB_TOKEN }}'
    plugin-slug: searchwiz
    plugin-path: src/searchwiz
    checks: |
      plugin_header
      file_type
      plugin_updater
```

**Why this works:**
- Uses official WordPress plugin check action
- Validates against WordPress.org requirements
- Produces detailed reports

**Time:** 15 minutes (includes testing)

---

### Option 3: Use Docker-based WordPress CLI

**Replace lines 36-40 with:**
```yaml
- name: Run WordPress Plugin Check
  run: |
    docker run --rm \
      -v ${{ github.workspace }}/src/searchwiz:/plugin \
      wordpress:cli wp plugin check /plugin \
      --format=json \
      --fields=type,message || true
```

**Why this works:**
- Uses official WordPress CLI Docker image
- Can run actual plugin validation
- Flexible for future plugin tests

**Time:** 10 minutes

---

## Acceptance Criteria

- [ ] `.github/workflows/plugin-check.yml` runs without errors
- [ ] Recent commit triggers workflow and shows ✅ success or ⚠️ warning (not ❌ failure)
- [ ] PR created with fix
- [ ] Build status on master branch shows green
- [ ] No breaking changes to other workflows (lint, tests, release)

---

## Testing Instructions

After making changes:

```bash
# 1. Commit changes to feature branch
git checkout -b fix/wp-004-plugin-check-workflow
git add .github/workflows/plugin-check.yml
git commit -m "fix(ci): Fix plugin-check workflow syntax error"
git push origin fix/wp-004-plugin-check-workflow

# 2. Create PR
gh pr create \
  --title "fix(ci): Fix plugin-check workflow - remove broken WordPress action" \
  --body "Fixes WP-004: Removes WordPress/WordPress@master action that doesn't exist"

# 3. Verify workflow runs
gh pr checks --watch

# 4. If green, merge
gh pr merge --squash --delete-branch
```

---

## Dependencies

**Blocks:**
- All agent work (build health checks fail)
- WP-001 (WordPress.org fixes - need green build)
- Any PR merges (failing status checks)

**Depends On:**
- None (can start immediately)

---

## Estimated Time

- **Option 1 (Recommended):** 5-10 minutes
- **Option 2:** 15-20 minutes
- **Option 3:** 10-15 minutes

---

## DevOps Agent Instructions

1. Read this file completely
2. Choose **Option 1** (fastest, safest)
3. Edit `.github/workflows/plugin-check.yml` - comment out or remove lines 36-40
4. Test locally if possible: `act -j plugin-check` (if act installed)
5. Create feature branch: `fix/wp-004-plugin-check-workflow`
6. Commit with message: `fix(ci): Remove broken WordPress/WordPress@master action`
7. Push and create PR
8. Update `.claude/progress/features.json` - set WP-004 status to "in_progress"
9. After PR created, update status to "review"
10. Write completion message to `.claude/progress/messages/devops-to-lead.md`

---

## Human Action Required

**After DevOps Agent Creates PR:**
1. Review PR
2. Verify workflow runs and passes
3. Merge PR
4. Confirm master branch build is green
5. Delete this URGENT file: `rm .claude/progress/URGENT-WP-004.md`

---

**CRITICAL: This blocks all other agent work. Fix immediately before launching other agents.**
