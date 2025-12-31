# Autobuild.ai Creator Guide

> **How to Build and Maintain the Autobuild.ai Course** — A comprehensive guide for course creators covering infrastructure, content creation, and community management

---

## Table of Contents

1. [Overview](#overview)
2. [Strategic Rationale](#strategic-rationale)
3. [Repository Architecture](#repository-architecture)
4. [GitHub Platform Setup](#github-platform-setup)
5. [GitHub Pages Configuration](#github-pages-configuration)
6. [GitHub Actions Workflows](#github-actions-workflows)
7. [GitHub Discussions Setup](#github-discussions-setup)
8. [Content Creation Pipeline](#content-creation-pipeline)
9. [Multi-Agent Development Workflow](#multi-agent-development-workflow)
10. [Video Production](#video-production)
11. [Licensing Strategy](#licensing-strategy)
12. [Community Management](#community-management)
13. [Governance and Contributions](#governance-and-contributions)
14. [Conflict of Interest Safeguards](#conflict-of-interest-safeguards)
15. [Implementation Phases](#implementation-phases)
16. [Quick Start Commands](#quick-start-commands)

---

## Overview

This document is for **course creators and maintainers** — not students. It covers:

- How to set up and maintain the course infrastructure
- The multi-agent workflow for creating content
- GitHub configuration, Actions, and community management
- Video production and publishing
- Licensing, governance, and conflict of interest considerations

For the actual course content (modules, lessons, learning outcomes), see `autobuild-course-content.md`.

---

## Strategic Rationale

### Why Open Source?

1. **Eliminates conflict of interest** — No profit motive removes ethical concerns about monetizing employer-adjacent knowledge
2. **Aligns with nonprofit values** — Knowledge sharing and community benefit
3. **Builds reputation** — Open source contributors are highly respected in the tech community
4. **Creates network effects** — Contributors, students, and users become professional connections
5. **Generates opportunities** — Speaking, consulting, and career advancement

### Expected Indirect Benefits

- Professional reputation and thought leadership
- Conference speaking invitations
- Consulting inquiries from companies implementing Agentic AI
- Networking with other practitioners and educators
- Potential book deal or other publishing opportunities
- Career advancement and visibility

---

## Repository Architecture

### Complete Directory Structure

```
autobuild-ai/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml
│   │   ├── content_suggestion.yml
│   │   ├── lesson_feedback.yml
│   │   └── question.yml
│   ├── DISCUSSION_TEMPLATE/
│   │   └── question.yml
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── CODEOWNERS
│   ├── FUNDING.yml
│   ├── dependabot.yml
│   └── workflows/
│       ├── deploy.yml              # Deploy to GitHub Pages
│       ├── test-code.yml           # Test Python examples
│       ├── check-links.yml         # Verify all links work
│       ├── welcome.yml             # Greet new contributors
│       └── stale.yml               # Manage stale issues
│
├── docs/                           # MkDocs source (course content)
│   ├── index.md                    # Course homepage
│   ├── prerequisites.md            # Setup guide
│   ├── learning-path.md            # Recommended order
│   │
│   ├── module-01-how-it-works/
│   │   ├── index.md
│   │   ├── 01-end-of-learn-to-code.md
│   │   ├── 02-how-agents-build.md
│   │   ├── 03-your-role.md
│   │   ├── 04-the-toolkit.md
│   │   ├── 05-what-you-can-build.md
│   │   └── 06-environment-setup.md
│   │
│   ├── module-02-spec-templates/
│   │   ├── index.md
│   │   ├── 01-the-template.md
│   │   ├── 02-describing-your-app.md
│   │   ├── 03-listing-features.md
│   │   ├── 04-defining-data.md
│   │   ├── 05-business-rules.md
│   │   ├── 06-success-criteria.md
│   │   └── 07-common-mistakes.md
│   │
│   ├── module-03-first-autobuild/
│   │   ├── index.md
│   │   ├── 01-full-flow.md
│   │   ├── 02-feeding-the-spec.md
│   │   ├── 03-watching-ai-build.md
│   │   ├── 04-qa-checks.md
│   │   ├── 05-reviewing-results.md
│   │   ├── 06-refining.md
│   │   └── 07-now-what.md
│   │
│   ├── module-04-ai-team/
│   │   ├── index.md
│   │   ├── 01-why-multiple-agents.md
│   │   ├── 02-dev-agent.md
│   │   ├── 03-qa-agent.md
│   │   ├── 04-review-agent.md
│   │   ├── 05-docs-agent.md
│   │   ├── 06-handoffs.md
│   │   └── 07-when-to-step-in.md
│   │
│   ├── module-05-going-live/
│   │   ├── index.md
│   │   ├── 01-production-ready.md
│   │   ├── 02-cost-management.md
│   │   ├── 03-security-basics.md
│   │   ├── 04-error-handling.md
│   │   ├── 05-deployment-options.md
│   │   ├── 06-monitoring.md
│   │   ├── 07-maintenance.md
│   │   └── 08-when-to-hire-devs.md
│   │
│   ├── module-06-advanced/
│   │   ├── index.md
│   │   ├── 01-external-apis.md
│   │   ├── 02-database-design.md
│   │   ├── 03-authentication.md
│   │   ├── 04-adding-ai-features.md
│   │   ├── 05-mobile-multiplatform.md
│   │   └── 06-mcp-extensibility.md
│   │
│   ├── module-07-capstone/
│   │   ├── index.md
│   │   ├── project-options.md
│   │   ├── submission-guide.md
│   │   └── showcase.md
│   │
│   ├── resources/
│   │   ├── glossary.md
│   │   ├── reading-list.md
│   │   ├── tools-comparison.md
│   │   └── cheatsheets/
│   │       ├── spec-writing.md
│   │       ├── ai-prompting.md
│   │       └── deployment.md
│   │
│   └── includes/
│       └── abbreviations.md
│
├── templates/                      # THE CORE DELIVERABLE
│   ├── README.md                   # How to use templates
│   ├── spec-template.md            # Main spec template
│   ├── spec-template-simple.md     # Simplified version
│   ├── spec-template-advanced.md   # For complex apps
│   └── examples/
│       ├── task-tracker/
│       │   └── spec.md
│       ├── booking-system/
│       │   └── spec.md
│       ├── client-portal/
│       │   └── spec.md
│       └── dashboard/
│           └── spec.md
│
├── builds/                         # Example autobuilt apps
│   ├── task-tracker/
│   │   ├── spec/                   # The spec that created it
│   │   ├── app/                    # The generated app
│   │   └── README.md               # How it was built
│   └── booking-system/
│       ├── spec/
│       ├── app/
│       └── README.md
│
├── exercises/                      # Practice problems
│   ├── module-02/
│   │   ├── exercise-01-user-story.md
│   │   └── solutions/
│   │       └── exercise-01-solution.md
│   └── ...
│
├── tests/                          # Validates spec templates and build outputs
│   ├── conftest.py
│   ├── test_spec_validation.py     # Ensures spec templates are well-formed
│   └── test_build_outputs.py       # Smoke tests for example builds
│
├── scripts/                        # Development utilities
│   ├── setup_dev.sh
│   ├── start-agents.sh             # Multi-agent tmux session
│   ├── check_links.py
│   └── validate_specs.py
│
├── .gitignore
├── .python-version
├── README.md                       # Repository overview
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── LICENSE                         # MIT for code
├── LICENSE-CONTENT                 # CC-BY-4.0 for content
├── CHANGELOG.md
├── mkdocs.yml                      # Site configuration
└── requirements-docs.txt           # MkDocs dependencies
```

### File Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Lessons | `XX-title-kebab-case.md` | `01-spec-first-vs-vibe-coding.md` |
| Specs | Descriptive name | `requirements.md`, `design.md` |
| Exercises | `exercise-XX-topic.md` | `exercise-01-user-story.md` |
| Projects | Directory with spec + src | `task-manager/spec/`, `task-manager/src/` |

---

## GitHub Platform Setup

### Why GitHub for Course Hosting?

| Benefit | How It Helps Your Course |
|---------|--------------------------|
| **Discovery** | 100M+ developers already on GitHub, searchable |
| **Credibility** | Stars/forks signal quality to the community |
| **Collaboration** | Built-in PRs, issues, discussions |
| **Free hosting** | GitHub Pages = $0 website hosting |
| **Version control** | Track all changes, easy rollbacks |
| **CI/CD** | Auto-deploy, auto-test with Actions |

### GitHub Pro Benefits ($4/month)

| Feature | How You'll Use It |
|---------|-------------------|
| **Required reviewers** | Ensure quality on PRs from contributors |
| **Protected branches** | Prevent accidental pushes to main |
| **Repository insights** | Traffic analytics, clone stats, referrers |
| **3,000 Actions minutes/month** | More CI/CD capacity for testing |
| **Code owners** | Auto-assign reviewers by file path |
| **Multiple reviewers** | Scale as contributors grow |
| **Draft pull requests** | Work in progress visibility |

**Most valuable:** Repository insights, protected branches, and extra Actions minutes.

### Monthly Costs

| Service | Cost |
|---------|------|
| GitHub Pro | $4/month |
| GitHub Pages | Free |
| GitHub Actions | Free (3,000 min/month with Pro) |
| GitHub Discussions | Free |
| YouTube | Free |
| Custom domain (optional) | ~$12/year |
| Claude Code API | ~$20-50/month |
| **Total** | **~$24-54/month** |

---

## GitHub Pages Configuration

### MkDocs Configuration

```yaml
# mkdocs.yml
site_name: Autobuild.ai
site_url: https://[username].github.io/autobuild-ai
site_description: Your Spec, AI's Creation — Build production apps without writing code
site_author: [Your Name]
repo_url: https://github.com/[username]/autobuild-ai
repo_name: "[username]/autobuild-ai"
edit_uri: edit/main/docs/

copyright: |
  Content licensed under <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>.
  Code licensed under <a href="https://opensource.org/licenses/MIT">MIT</a>.

theme:
  name: material
  custom_dir: docs/overrides
  logo: assets/logo.png
  favicon: assets/favicon.png

  features:
    - navigation.tabs
    - navigation.tabs.sticky
    - navigation.sections
    - navigation.expand
    - navigation.path
    - navigation.top
    - navigation.footer
    - search.suggest
    - search.highlight
    - search.share
    - content.code.copy
    - content.code.annotate
    - content.tabs.link
    - toc.follow
    - announce.dismiss

  palette:
    - scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: Switch to light mode

  font:
    text: Inter
    code: JetBrains Mono

  icon:
    repo: fontawesome/brands/github

extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/[username]
    - icon: fontawesome/brands/linkedin
      link: https://linkedin.com/in/[username]
    - icon: fontawesome/brands/youtube
      link: https://youtube.com/@[channel]

  analytics:
    provider: google
    property: G-XXXXXXXXXX

  consent:
    title: Cookie consent
    description: >-
      We use cookies to recognize your repeated visits and preferences,
      as well as to measure the effectiveness of our documentation.

extra_css:
  - stylesheets/extra.css

markdown_extensions:
  - abbr
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - toc:
      permalink: true
      toc_depth: 3
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.details
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.snippets:
      auto_append:
        - docs/includes/abbreviations.md
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tabbed:
      alternate_style: true
      slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde

plugins:
  - search:
      separator: '[\s\-,:!=\[\]()"/]+|(?!\b)(?=[A-Z][a-z])|\.(?!\d)|&[lg]t;'
  - git-revision-date-localized:
      enable_creation_date: true
      type: timeago
  - git-committers:
      repository: [username]/autobuild-ai
      branch: main
  - minify:
      minify_html: true

nav:
  - Home: index.md
  - Getting Started:
    - Prerequisites: prerequisites.md
    - Learning Path: learning-path.md
  - Modules:
    - "1. How Autobuild Works":
      - Overview: module-01-how-it-works/index.md
      - The End of Learn-to-Code: module-01-how-it-works/01-end-of-learn-to-code.md
      - How Agents Build: module-01-how-it-works/02-how-agents-build.md
      - Your Role: module-01-how-it-works/03-your-role.md
      - The Toolkit: module-01-how-it-works/04-the-toolkit.md
      - What You Can Build: module-01-how-it-works/05-what-you-can-build.md
      - Environment Setup: module-01-how-it-works/06-environment-setup.md
    - "2. The Spec Templates":
      - Overview: module-02-spec-templates/index.md
      - The Template: module-02-spec-templates/01-the-template.md
      - Describing Your App: module-02-spec-templates/02-describing-your-app.md
      - Listing Features: module-02-spec-templates/03-listing-features.md
      - Defining Data: module-02-spec-templates/04-defining-data.md
      - Business Rules: module-02-spec-templates/05-business-rules.md
      - Success Criteria: module-02-spec-templates/06-success-criteria.md
      - Common Mistakes: module-02-spec-templates/07-common-mistakes.md
    - "3. Your First Autobuild":
      - Overview: module-03-first-autobuild/index.md
      - The Full Flow: module-03-first-autobuild/01-full-flow.md
      - Feeding the Spec: module-03-first-autobuild/02-feeding-the-spec.md
      - Watching AI Build: module-03-first-autobuild/03-watching-ai-build.md
      - QA Checks: module-03-first-autobuild/04-qa-checks.md
      - Reviewing Results: module-03-first-autobuild/05-reviewing-results.md
      - Refining: module-03-first-autobuild/06-refining.md
      - Now What?: module-03-first-autobuild/07-now-what.md
    - "4. The AI Team":
      - Overview: module-04-ai-team/index.md
      - Why Multiple Agents: module-04-ai-team/01-why-multiple-agents.md
      - The Dev Agent: module-04-ai-team/02-dev-agent.md
      - The QA Agent: module-04-ai-team/03-qa-agent.md
      - The Review Agent: module-04-ai-team/04-review-agent.md
      - The Docs Agent: module-04-ai-team/05-docs-agent.md
      - Handoffs: module-04-ai-team/06-handoffs.md
      - When to Step In: module-04-ai-team/07-when-to-step-in.md
    - "5. Going Live":
      - Overview: module-05-going-live/index.md
      - Production-Ready: module-05-going-live/01-production-ready.md
      - Cost Management: module-05-going-live/02-cost-management.md
      - Security Basics: module-05-going-live/03-security-basics.md
      - Error Handling: module-05-going-live/04-error-handling.md
      - Deployment Options: module-05-going-live/05-deployment-options.md
      - Monitoring: module-05-going-live/06-monitoring.md
      - Maintenance: module-05-going-live/07-maintenance.md
      - When to Hire Devs: module-05-going-live/08-when-to-hire-devs.md
    - "6. Advanced":
      - Overview: module-06-advanced/index.md
      - External APIs: module-06-advanced/01-external-apis.md
      - Database Design: module-06-advanced/02-database-design.md
      - Authentication: module-06-advanced/03-authentication.md
      - Adding AI Features: module-06-advanced/04-adding-ai-features.md
      - Mobile & Multi-Platform: module-06-advanced/05-mobile-multiplatform.md
      - MCP Extensibility: module-06-advanced/06-mcp-extensibility.md
    - "7. Capstone":
      - Overview: module-07-capstone/index.md
      - Project Options: module-07-capstone/project-options.md
      - Submission Guide: module-07-capstone/submission-guide.md
      - Showcase: module-07-capstone/showcase.md
  - Templates:
    - Overview: templates/README.md
    - Main Template: templates/spec-template.md
    - Examples: templates/examples/
  - Resources:
    - Glossary: resources/glossary.md
    - Reading List: resources/reading-list.md
    - Tools Comparison: resources/tools-comparison.md
    - Cheatsheets:
      - Spec Writing: resources/cheatsheets/spec-writing.md
      - AI Prompting: resources/cheatsheets/ai-prompting.md
      - Deployment: resources/cheatsheets/deployment.md
  - Community:
    - Contributing: CONTRIBUTING.md
    - Code of Conduct: CODE_OF_CONDUCT.md
    - Discussions: https://github.com/[username]/autobuild-ai/discussions
```

### MkDocs Dependencies

```txt
# requirements-docs.txt
mkdocs>=1.5.0
mkdocs-material>=9.5.0
mkdocs-git-revision-date-localized-plugin>=1.2.0
mkdocs-git-committers-plugin-2>=2.2.0
mkdocs-minify-plugin>=0.8.0
pillow>=10.0.0
cairosvg>=2.7.0
```

### Enable GitHub Pages

1. Go to repository **Settings** → **Pages**
2. Under "Build and deployment":
   - Source: **GitHub Actions**
3. The deploy workflow will handle the rest

### Custom Domain (Optional)

1. Add `CNAME` file to `docs/` folder:
   ```
   course.yourdomain.com
   ```

2. Configure DNS:
   ```
   Type: CNAME
   Name: course
   Value: [username].github.io
   ```

3. Enable HTTPS in repository Settings → Pages

---

## GitHub Actions Workflows

### Workflow 1: Deploy to GitHub Pages

```yaml
# .github/workflows/deploy.yml
name: Deploy Course Site

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'
      - 'mkdocs.yml'
      - '.github/workflows/deploy.yml'
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          cache: 'pip'

      - name: Install dependencies
        run: pip install -r requirements-docs.txt

      - name: Build MkDocs site
        run: mkdocs build --strict

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: site/

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Workflow 2: Test Code Examples

```yaml
# .github/workflows/test-code.yml
name: Test Code Examples

on:
  push:
    branches: [main]
    paths:
      - 'builds/**'
      - 'tests/**'
  pull_request:
    branches: [main]
    paths:
      - 'builds/**'
      - 'tests/**'
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ['3.10', '3.11', '3.12']

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Python ${{ matrix.python-version }}
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
          cache: 'pip'

      - name: Install dependencies
        run: |
          pip install pytest pytest-asyncio

      - name: Run tests
        run: pytest tests/ -v --tb=short
```

### Workflow 3: Check Links

```yaml
# .github/workflows/check-links.yml
name: Check Links

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 0 * * 0'
  workflow_dispatch:

jobs:
  check-links:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Link Checker
        uses: lycheeverse/lychee-action@v1
        with:
          args: >-
            --verbose
            --no-progress
            --accept 200,204,206
            --timeout 30
            --max-retries 3
            --exclude-mail
            './docs/**/*.md'
            './README.md'
          fail: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Workflow 4: Welcome New Contributors

```yaml
# .github/workflows/welcome.yml
name: Welcome New Contributors

on:
  issues:
    types: [opened]
  pull_request_target:
    types: [opened]

jobs:
  welcome:
    runs-on: ubuntu-latest
    permissions:
      issues: write
      pull-requests: write
    steps:
      - uses: actions/first-interaction@v1
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
          issue-message: |
            Thanks for opening your first issue!

            We appreciate you taking the time to contribute to Autobuild.ai.

            **What happens next:**
            - A maintainer will review your issue
            - Please provide as much detail as possible
            - Check out our [Contributing Guide](CONTRIBUTING.md)

            Happy building!

          pr-message: |
            Thanks for your first pull request!

            We're excited to have you contribute to Autobuild.ai.

            **Checklist:**
            - [ ] Code follows the style guide
            - [ ] Tests pass locally
            - [ ] Documentation updated (if needed)

            A maintainer will review your PR soon. Thanks for helping make this course better!
```

### Workflow 5: Stale Issue Management

```yaml
# .github/workflows/stale.yml
name: Manage Stale Issues

on:
  schedule:
    - cron: '0 0 * * *'
  workflow_dispatch:

jobs:
  stale:
    runs-on: ubuntu-latest
    permissions:
      issues: write
      pull-requests: write
    steps:
      - uses: actions/stale@v9
        with:
          stale-issue-message: |
            This issue has been automatically marked as stale because it has not had
            recent activity. It will be closed in 14 days if no further activity occurs.

            If this issue is still relevant, please comment to keep it open.

          stale-pr-message: |
            This PR has been automatically marked as stale because it has not had
            recent activity. It will be closed in 14 days if no further activity occurs.

          stale-issue-label: 'stale'
          stale-pr-label: 'stale'
          days-before-stale: 60
          days-before-close: 14
          exempt-issue-labels: 'pinned,help wanted,good first issue'
```

---

## GitHub Discussions Setup

### Enable Discussions

1. Go to repository **Settings**
2. Scroll to **Features**
3. Check **Discussions**

### Configure Discussion Categories

| Category | Icon | Format | Description |
|----------|------|--------|-------------|
| **Announcements** | :mega: | Announcement | Course updates, new modules |
| **General** | :speech_balloon: | Open | Community discussion |
| **Ideas** | :bulb: | Open | Feature requests, suggestions |
| **Q&A** | :pray: | Question/Answer | Help with lessons, code issues |
| **Show and Tell** | :raised_hands: | Open | Share your projects, wins |
| **Module 1** | :books: | Question/Answer | How Autobuild Works questions |
| **Module 2** | :books: | Question/Answer | Spec Templates questions |
| **Module 3** | :books: | Question/Answer | First Autobuild questions |
| **Module 4** | :books: | Question/Answer | AI Team questions |
| **Module 5** | :books: | Question/Answer | Going Live questions |
| **Module 6** | :books: | Question/Answer | Advanced topics questions |
| **Capstone** | :books: | Open | Capstone project discussion |

### Pinned Discussions

Create and pin:

1. **Welcome & Course Overview** — Getting started, community guidelines, quick links
2. **FAQ - Start Here** — Common questions and answers

### Discussion Template

```yaml
# .github/DISCUSSION_TEMPLATE/question.yml
title: "[Q&A] "
labels: ["question"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for asking a question! Please fill out the details below.

  - type: dropdown
    id: module
    attributes:
      label: Which module is this related to?
      options:
        - Module 1 - How Autobuild Works
        - Module 2 - Spec Templates
        - Module 3 - First Autobuild
        - Module 4 - AI Team
        - Module 5 - Going Live
        - Module 6 - Advanced
        - Capstone
        - General / Not specific
    validations:
      required: true

  - type: textarea
    id: question
    attributes:
      label: Your Question
      description: What do you need help with?
      placeholder: Describe your question clearly...
    validations:
      required: true

  - type: textarea
    id: context
    attributes:
      label: What have you tried?
      description: Share any code, errors, or things you've already attempted.
```

---

## Content Creation Pipeline

### Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     CONTENT CREATION WITH CLAUDE CODE + TMUX             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐            │
│   │ DIRECTOR │──►│  AUTHOR  │──►│ REVIEWER │──►│PUBLISHER │            │
│   │  (Opus)  │   │ (Sonnet) │   │ (Sonnet) │   │ (Haiku)  │            │
│   └──────────┘   └──────────┘   └──────────┘   └──────────┘            │
│       │              │              │              │                    │
│       ▼              ▼              ▼              ▼                    │
│   • Define      • Write        • Validate     • Commit                 │
│     outline       lesson         content       changes                 │
│   • Set         • Create       • Run code    • Push to                 │
│     objectives    examples       examples      GitHub                  │
│   • Approve     • Generate     • Check       • Monitor                 │
│     structure     exercises      links         deploy                  │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Per-Lesson Creation Checklist

```markdown
## Lesson Creation Checklist

### Planning (Director Agent)
- [ ] Define 2-3 specific learning objectives
- [ ] Identify prerequisite knowledge
- [ ] List key concepts to cover
- [ ] Plan examples needed
- [ ] Estimate duration (target: 10-20 min)

### Content Creation (Author Agent)
- [ ] Write lesson content in Markdown
- [ ] Create practical examples
- [ ] Add exercise or reflection questions
- [ ] Create any diagrams (Mermaid or images)

### Validation (Reviewer Agent)
- [ ] Content matches objectives
- [ ] Examples are accurate and clear
- [ ] All links working
- [ ] Formatting correct for MkDocs
- [ ] Spelling/grammar checked

### Deployment (Publisher Agent)
- [ ] Commit to repository
- [ ] Push to GitHub
- [ ] Verify GitHub Pages deployment
- [ ] Check live site renders correctly

### Final Review (Director Agent)
- [ ] Approve for publication
- [ ] Update changelog
- [ ] Draft announcement (Discussions)
```

---

## Multi-Agent Development Workflow

### Why Claude Code + Tmux?

| Factor | Benefit |
|--------|---------|
| **Consistency** | Same setup used across projects |
| **Parallel work** | Multiple agents working simultaneously |
| **200K context** | Entire modules fit in memory |
| **Proven pattern** | Production-tested on real projects |
| **Teachable** | We can show students exactly how we built the course |
| **Cost-effective** | Usage-based, no per-seat licensing |

### Tmux Session Layout (Separate Windows)

Each agent runs in its own tmux window for easy switching:

```
Session: autobuild
├── Window 0: DIRECTOR (Opus)     ← Ctrl+B 0
│   • Coordinates work
│   • Reviews specs
│   • Makes decisions
│
├── Window 1: AUTHOR (Sonnet)     ← Ctrl+B 1
│   • Writes code/content
│   • Implements features
│   • Creates examples
│
├── Window 2: REVIEWER (Sonnet)   ← Ctrl+B 2
│   • Validates output
│   • Checks quality
│   • Runs link checker
│
└── Window 3: PUBLISHER (Haiku)   ← Ctrl+B 3
    • Deploys to GitHub
    • Manages workflows
    • Monitors builds

Navigation:
  Ctrl+B 0-3    Jump to window by number
  Ctrl+B n      Next window
  Ctrl+B p      Previous window
  Ctrl+B w      List all windows (interactive)
```

### Agent Responsibilities

| Agent | Model | Primary Tasks | Example Prompts |
|-------|-------|--------------|-----------------|
| **Director** | Opus | Coordination, specs, decisions, final approval | "Review Module 2 outline and identify gaps" |
| **Author** | Sonnet | Content writing, code examples, exercises | "Write lesson 2.3 on defining constraints" |
| **Reviewer** | Sonnet | Quality assurance, links, validation | "Check all code examples in Module 2 run correctly" |
| **Publisher** | Haiku | Deploy, CI/CD, monitoring, simple ops | "Push changes and verify GitHub Pages deployment" |

### Why These Model Choices?

| Agent | Model | Rationale |
|-------|-------|-----------|
| **Director** | Opus | Requires deep reasoning for course architecture decisions, handles complex trade-offs, ensures no blockers during content creation |
| **Author** | Sonnet | Strong balance of capability and cost for content generation, excellent at writing clear explanations and code |
| **Reviewer** | Sonnet | Needs good judgment for quality assessment, catches nuanced issues in content and code |
| **Publisher** | Haiku | Simple, repetitive tasks (git commands, deployment checks) don't require advanced reasoning, cost-efficient |

### Starting the Multi-Agent Session

```bash
#!/bin/bash
# scripts/start-agents.sh
#
# Creates a tmux session with 4 separate WINDOWS (not panes)
# for easier navigation between agents.
#
# Navigation:
#   Ctrl+B 0  → Director window
#   Ctrl+B 1  → Author window
#   Ctrl+B 2  → Reviewer window
#   Ctrl+B 3  → Publisher window
#   Ctrl+B w  → List all windows

SESSION="autobuild"
PROJECT_DIR="$HOME/projects/autobuild-ai"

# Kill existing session if any
tmux kill-session -t $SESSION 2>/dev/null

# Window 0: Director Agent (Opus model for complex decisions)
tmux new-session -d -s $SESSION -n "DIRECTOR"
tmux send-keys -t $SESSION:0 "cd $PROJECT_DIR && claude --model opus" Enter

# Window 1: Author Agent (Sonnet model for content creation)
tmux new-window -t $SESSION -n "AUTHOR"
tmux send-keys -t $SESSION:1 "cd $PROJECT_DIR && claude --model sonnet" Enter

# Window 2: Reviewer Agent (Sonnet model for quality checks)
tmux new-window -t $SESSION -n "REVIEWER"
tmux send-keys -t $SESSION:2 "cd $PROJECT_DIR && claude --model sonnet" Enter

# Window 3: Publisher Agent (Haiku model for simple ops)
tmux new-window -t $SESSION -n "PUBLISHER"
tmux send-keys -t $SESSION:3 "cd $PROJECT_DIR && claude --model haiku" Enter

# Go back to Director window (window 0)
tmux select-window -t $SESSION:0

# Attach to session
tmux attach -t $SESSION
```

### Tmux Configuration

```bash
# ~/.tmux.conf additions for multi-agent work

# Quick window switching with Alt+number (no prefix needed)
bind-key -n M-0 select-window -t 0
bind-key -n M-1 select-window -t 1
bind-key -n M-2 select-window -t 2
bind-key -n M-3 select-window -t 3

# Increase scrollback for long agent outputs
set -g history-limit 50000

# Mouse support for easy window switching
set -g mouse on

# Show window names in status bar
set -g status-left "[#S] "
set -g window-status-format "#I:#W"
set -g window-status-current-format "#[fg=green,bold]#I:#W"
```

### Agent Handoff Pattern

```
DIRECTOR (Opus): "Create lesson on acceptance criteria"
    │
    ▼
AUTHOR (Sonnet):
    • Writes lesson markdown
    • Creates code examples
    • Generates exercise
    │
    ▼
REVIEWER (Sonnet):
    • Reviews for accuracy
    • Runs code examples
    • Checks links
    • Validates formatting
    │
    ▼
PUBLISHER (Haiku):
    • Commits to feature branch
    • Creates PR
    • Monitors deployment
    • Verifies live site
    │
    ▼
DIRECTOR (Opus):
    • Final review
    • Merge approval
```

---

## Video Production

### Recommended Tools

| Purpose | Free Option | Paid Option |
|---------|-------------|-------------|
| **Screen Recording** | OBS Studio | Camtasia |
| **Avatar Generation** | D-ID free tier | HeyGen, Synthesia |
| **Video Editing** | DaVinci Resolve | Premiere Pro |
| **Thumbnails** | Canva Free | Canva Pro |
| **Hosting** | YouTube | YouTube |

### Video Format Specification

```yaml
Format:
  Resolution: 1920x1080 (1080p)
  Frame Rate: 30fps
  Aspect Ratio: 16:9
  Export: MP4 (H.264)

Layout:
  Screen content with corner avatar (200x200px, bottom-right)

Audio:
  - Clear narration
  - Consistent volume (-14 LUFS)
  - No background music (or very subtle)

Captions:
  - Auto-generated via YouTube
  - Review and correct errors
  - Download SRT for repository
```

### YouTube Setup

1. **Create Playlist:** "Autobuild.ai"
2. **Video Settings:**
   - Visibility: Unlisted (embed only) or Public
   - Category: Education
   - Tags: autobuild, ai agents, spec-first, no-code

### Embedding Videos in MkDocs

```markdown
<div class="video-wrapper">
  <iframe
    src="https://www.youtube.com/embed/VIDEO_ID"
    title="Lesson Title"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>
```

```css
/* docs/stylesheets/extra.css */
.video-wrapper {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  margin: 1rem 0;
}

.video-wrapper iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 8px;
}
```

---

## Licensing Strategy

### Dual License Approach

#### Code: MIT License

```
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

#### Content: Creative Commons Attribution 4.0

```
Creative Commons Attribution 4.0 International (CC BY 4.0)

Copyright (c) 2025 [Your Name]

You are free to:
* Share — copy and redistribute the material in any medium or format
* Adapt — remix, transform, and build upon the material for any purpose,
  even commercially

Under the following terms:
* Attribution — You must give appropriate credit, provide a link to the
  license, and indicate if changes were made.

Full license text: https://creativecommons.org/licenses/by/4.0/legalcode
```

---

## Community Management

### Platforms

| Platform | Purpose | Setup |
|----------|---------|-------|
| **GitHub Discussions** | Primary Q&A, announcements | Included |
| **YouTube** | Video hosting | Create playlist |
| **LinkedIn** | Professional updates | Personal account |
| **Twitter/X** | Quick updates | Optional |
| **Discord** | Real-time chat (optional) | Create if demand |

### Content Calendar

**Weekly Rhythm:**
- **Monday:** New content push (if ready)
- **Wednesday:** Discussion prompt or tip
- **Friday:** Community highlight

**Monthly:**
- First week: New module announcement
- Mid-month: Office hours (optional live)
- End of month: Progress summary

### Metrics to Track

| Metric | 3 Month | 6 Month | 12 Month |
|--------|---------|---------|----------|
| GitHub Stars | 500 | 1,200 | 2,500 |
| Forks | 100 | 300 | 600 |
| YouTube Views | 10,000 | 40,000 | 100,000 |
| YouTube Subscribers | 500 | 1,500 | 3,500 |
| Discussion Posts | 100 | 400 | 1,000 |
| Contributors | 10 | 25 | 50 |
| Capstone Submissions | 20 | 100 | 300 |

---

## Governance and Contributions

### CONTRIBUTING.md Template

```markdown
# Contributing to Autobuild.ai

Thank you for your interest in contributing! This course is community-driven,
and we welcome contributions of all kinds.

## Ways to Contribute

### Report Issues
- Typos or errors in content
- Broken links
- Code that doesn't work
- Unclear explanations

### Suggest Improvements
- New topics to cover
- Better explanations
- Additional examples
- Resource recommendations

### Submit Changes
- Fix typos or bugs
- Improve code examples
- Add exercises
- Translate content

## How to Contribute

### For Small Changes (typos, small fixes)
1. Click "Edit" on any page
2. Make your changes
3. Submit a pull request

### For Larger Changes
1. Open an issue first to discuss
2. Fork the repository
3. Create a feature branch: `git checkout -b feature/my-improvement`
4. Make your changes
5. Test locally: `mkdocs serve`
6. Commit with clear message
7. Push and open a pull request

## Code Style
- Python: Follow Black formatting
- Markdown: One sentence per line
- Code examples: Include comments

## Review Process
1. Automated checks run (tests, links)
2. Maintainer reviews within 1 week
3. Feedback provided if changes needed
4. Merged when approved
```

### CODEOWNERS

```
# .github/CODEOWNERS

# Default owner for everything
* @[username]

# Specific module owners (add as contributors join)
# /docs/module-03-first-autobuild/ @contributor1
# /docs/module-04-ai-team/ @contributor2
```

### Branch Protection Rules

Configure in Settings → Branches → Add rule for `main`:

- [x] Require a pull request before merging
- [x] Require status checks to pass
  - [x] Deploy Course Site
  - [x] Test Code Examples
  - [x] Check Links
- [x] Require conversation resolution
- [x] Include administrators

---

## Conflict of Interest Safeguards

### Guiding Principles

1. **No Proprietary Content** — All examples use public APIs and frameworks
2. **Balanced Coverage** — Multiple frameworks covered fairly
3. **Time Separation** — Personal time and equipment only
4. **Transparent Disclosure** — README includes disclosure statement

### Disclosure Statement (for README)

```markdown
## Disclosure

This course is a personal project created on my own time using my own
resources. It is not affiliated with, sponsored by, or endorsed by my
employer. All content is based on publicly available information and
my general professional experience in software architecture.

The views and opinions expressed in this course are my own and do not
represent the views of any organization I am affiliated with.
```

### Development Log (Private)

Keep a simple log (not in repo):

```markdown
# Development Log

## [Date]
- Equipment: Personal laptop
- Time: [start]-[end], weekend/evening
- Content created: [description]
- Work resources used: None
```

---

## Implementation Phases

### Phase 0: GitHub Setup

| Task | Details |
|------|---------|
| Create GitHub repository | `autobuild-ai`, public |
| Enable GitHub Pro features | Protected branches, insights |
| Add license files | MIT + CC-BY-4.0 |
| Create directory structure | As defined above |
| Set up MkDocs | Install, configure, test locally |
| Enable GitHub Pages | Source: GitHub Actions |
| Add GitHub Actions workflows | Deploy, test, links |
| Enable Discussions | Configure categories |
| Create issue templates | Bug, suggestion, question |
| Write README | Course overview, getting started |
| Write CONTRIBUTING | Contribution guidelines |
| Create CODE_OF_CONDUCT | Community standards |
| Configure branch protection | Require PR, status checks |

**Milestone:** Repository fully set up, site deploying

### Phase 1: Foundation

| Week | Tasks | Deliverables |
|------|-------|--------------|
| 1 | Write Module 1 outline, lessons 1-2 | 2 lessons drafted |
| 2 | Complete Module 1 (lessons 3-6) | Module 1 content complete |
| 3 | Create code examples for Module 1 | Code tested and committed |
| 4 | Record/generate videos for Module 1 | Videos on YouTube, embedded |

**Milestone:** Module 1 fully released with video content

### Phase 2: Core Content

| Weeks | Focus | Deliverables |
|-------|-------|--------------|
| 5-6 | Module 2: Spec Templates | 7 lessons + project |
| 7-8 | Module 3: First Autobuild | 7 lessons + project |
| 9-10 | Module 4: AI Team | 7 lessons + project |
| 11-12 | Module 5: Going Live | 8 lessons + project |

**Milestone:** Core curriculum complete (Modules 1-5)

### Phase 3: Advanced & Polish

| Week | Focus | Deliverables |
|------|-------|--------------|
| 13 | Module 6: Advanced Topics | 6 lessons complete |
| 14 | Module 7: Capstone setup | Project templates, guide |
| 15 | Review and polish all content | Fixes, improvements |
| 16 | Community launch | Announcements, promotion |

**Milestone:** Full course release

### Phase 4: Community & Iteration (Ongoing)

- Respond to issues and discussions
- Accept and review pull requests
- Add community-requested content
- Update for framework changes
- Showcase student projects
- Monthly analytics review

---

## Quick Start Commands

### Initial Repository Setup

```bash
# 1. Create repository on GitHub first, then:
git clone https://github.com/[username]/autobuild-ai.git
cd autobuild-ai

# 2. Create directory structure
mkdir -p .github/{ISSUE_TEMPLATE,DISCUSSION_TEMPLATE,workflows}
mkdir -p docs/{module-01-how-it-works,module-02-spec-templates,module-03-first-autobuild}
mkdir -p docs/{module-04-ai-team,module-05-going-live,module-06-advanced}
mkdir -p docs/{module-07-capstone,resources/cheatsheets,includes}
mkdir -p templates/examples
mkdir -p builds
mkdir -p tests
mkdir -p scripts

# 3. Create initial files
touch README.md CONTRIBUTING.md CODE_OF_CONDUCT.md CHANGELOG.md
touch LICENSE LICENSE-CONTENT
touch mkdocs.yml requirements-docs.txt
touch .gitignore .python-version
touch docs/index.md docs/prerequisites.md docs/learning-path.md
touch docs/includes/abbreviations.md
touch docs/resources/cheatsheets/{spec-writing,ai-prompting,deployment}.md
touch templates/README.md templates/spec-template.md
touch tests/conftest.py tests/test_spec_validation.py tests/test_build_outputs.py

# 4. Set up Python environment
python -m venv venv
source venv/bin/activate
pip install -r requirements-docs.txt

# 5. Test MkDocs locally
mkdocs serve
# Visit http://127.0.0.1:8000

# 6. Initial commit
git add .
git commit -m "Initial course structure"
git push origin main
```

### Start Multi-Agent Session

```bash
# Make executable (one time)
chmod +x scripts/start-agents.sh

# Start multi-agent session
./scripts/start-agents.sh

# Navigate between panes: Ctrl+B then arrow keys
# Detach: Ctrl+B then D
# Reattach: tmux attach -t autobuild
```

### Daily Development Commands

```bash
# Start multi-agent session
./scripts/start-agents.sh

# Start local development server (in separate terminal)
mkdocs serve

# Build site (check for errors)
mkdocs build --strict

# Check links locally
pip install linkchecker
linkchecker http://127.0.0.1:8000
```

### Deployment

Deployment is automatic via GitHub Actions when you push to `main`.

```bash
# Manual deploy (if needed)
mkdocs gh-deploy --force
```

---

## GitHub Issue Templates

### Bug Report

```yaml
# .github/ISSUE_TEMPLATE/bug_report.yml
name: Bug Report
description: Report an error or issue
title: "[Bug]: "
labels: ["bug", "triage"]
body:
  - type: markdown
    attributes:
      value: Thanks for reporting! Please fill out the details below.

  - type: dropdown
    id: type
    attributes:
      label: Type of issue
      options:
        - Code doesn't work
        - Broken link
        - Typo or error in content
        - Site/formatting issue
        - Other
    validations:
      required: true

  - type: input
    id: location
    attributes:
      label: Location
      description: Which lesson or file has the issue?
      placeholder: "e.g., Module 2, Lesson 3"
    validations:
      required: true

  - type: textarea
    id: description
    attributes:
      label: Description
      description: What's wrong?
    validations:
      required: true

  - type: textarea
    id: expected
    attributes:
      label: Expected behavior
      description: What should happen instead?
```

### Content Suggestion

```yaml
# .github/ISSUE_TEMPLATE/content_suggestion.yml
name: Content Suggestion
description: Suggest new content or improvements
title: "[Suggestion]: "
labels: ["enhancement"]
body:
  - type: dropdown
    id: type
    attributes:
      label: Suggestion type
      options:
        - New topic/lesson
        - Improve existing content
        - Add example
        - Add exercise
        - Other
    validations:
      required: true

  - type: textarea
    id: description
    attributes:
      label: Description
      description: What would you like to see?
    validations:
      required: true

  - type: textarea
    id: value
    attributes:
      label: Why is this valuable?
      description: How would this help learners?
```

---

## GitHub Sponsors (Optional)

### FUNDING.yml

```yaml
# .github/FUNDING.yml
github: [username]
```

### Sponsor Tiers

- **Coffee Supporter ($5/month):** Name in supporters list
- **Course Champion ($15/month):** Name + early access to new modules
- **Course Sponsor ($50/month):** Logo in README + all above

---

## Document Metadata

```yaml
Document: Autobuild.ai Creator Guide
Purpose: Course creation and maintenance documentation
Version: 1.0
Created: 2025

Development Stack:
  IDE: Claude Code (CLI) + Tmux
  Multi-Agent Pattern: Director → Author → Reviewer → Publisher
  Version Control: Git + GitHub
  Deployment: GitHub Actions → GitHub Pages
  Video Hosting: YouTube

Agent Models:
  Director: Claude Opus (complex decisions, coordination, final approval)
  Author: Claude Sonnet (content creation, code examples)
  Reviewer: Claude Sonnet (quality assurance, validation)
  Publisher: Claude Haiku (deployment, simple operations)

Monthly Costs:
  Claude Code API: ~$20-50 (usage-based)
  GitHub Pro: $4
  Hosting: Free (GitHub Pages)
  Videos: Free (YouTube)
  Total: ~$24-54/month
```

---

**Ready to build the course! Start with the Quick Start Commands section.**
