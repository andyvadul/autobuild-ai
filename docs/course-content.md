# Autobuild.ai Course Content

> **Your Spec, AI's Creation** — Build YOUR production-ready application by writing specifications while AI handles all the code

---

## Table of Contents

1. [Course Overview](#course-overview)
2. [Who This Course Is For](#who-this-course-is-for)
3. [The Autobuild Methodology](#the-autobuild-methodology)
4. [Course Modules](#course-modules)
5. [Spec Templates](#spec-templates)
6. [Resources](#resources)

---

## Course Overview

### Mission Statement

Enable business professionals to build THEIR OWN production-ready applications without writing code. You bring a real problem to solve. We give you the methodology, templates, and guidance to build it — module by module — until you deploy it live.

### How This Course Works

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│   MODULES 1-2: Identify YOUR idea + Write YOUR spec                      │
│        │                                                                 │
│        ▼                                                                 │
│   MODULES 3-4: Build a prototype (Claude Web → Claude Code)              │
│        │                                                                 │
│        ▼                                                                 │
│   MODULES 5-6: Hand off to AI Agents + Monitor their work                │
│        │                                                                 │
│        ▼                                                                 │
│   MODULES 7-8: Go multi-agent + Production hardening                     │
│        │                                                                 │
│        ▼                                                                 │
│   MODULES 9-10: Deploy YOUR app + What's next                            │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### What Makes This Different

| Aspect | Autobuild.ai | Typical AI/Coding Courses |
|--------|--------------|---------------------------|
| **What You Build** | YOUR app (your idea, your problem) | Follow-along tutorial app |
| **Your Role** | Think about business, fill in templates | Learn to code |
| **AI's Role** | Writes ALL the code | Assists your coding |
| **You Touch Code?** | Never | Yes, constantly |
| **Output** | YOUR app, deployed and live | Portfolio exercise you'll never use |
| **Format** | 10 micro-modules, 5 lessons each | Dense, hour-long lectures |

### The Reference Example: Task Tracker

Throughout the course, we use a **Task Tracker** as a reference example. You can:
- Look at its spec to understand how to write yours
- Compare your app's progress to it
- Use it as a fallback if you get stuck

But **you're not building the task tracker** — you're building YOUR app.

---

## Who This Course Is For

### Primary Personas

#### 1. Business Operators / Managers
- **Background:** Run teams, processes, or departments
- **Technical level:** Comfortable with spreadsheets, basic automation (Zapier, etc.)
- **Goal:** Build internal tools and automate workflows
- **What they'll build:** Custom dashboards, approval workflows, team trackers

#### 2. Founders / Entrepreneurs
- **Background:** Building a business, wearing many hats
- **Technical level:** Can read code, maybe write basic scripts
- **Goal:** Build MVPs and prototypes without hiring developers
- **What they'll build:** Customer portals, booking systems, marketplaces

#### 3. Product Managers / Business Analysts
- **Background:** Write requirements, manage backlogs, work with dev teams
- **Technical level:** Understand software concepts, limited coding
- **Goal:** Prototype ideas, build proof-of-concepts, reduce dev dependency
- **What they'll build:** Feature prototypes, internal tools, data dashboards

#### 4. Citizen Developers
- **Background:** IT-adjacent roles, power users
- **Technical level:** Some coding, comfortable with low-code tools
- **Goal:** Level up from no-code/low-code to production apps
- **What they'll build:** Anything their business needs

### Prerequisites

**Required:**
- **A real app idea** — Something you actually want to build
- Ability to dictate/write clear requirements (what you want built)
- Basic understanding of how software works (not how to code it)
- Willingness to iterate and refine specs

**NOT Required:**
- Programming experience
- Computer science background
- Previous AI/ML knowledge
- Command line experience (we'll teach you what you need)

---

## The Autobuild Methodology

### The Three-Phase Pipeline

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     THE AUTOBUILD PIPELINE                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   PHASE 1: SPEC + PROTOTYPE (You + Claude Web)                          │
│   ─────────────────────────────────────────────                          │
│   ┌─────────────────────────────────────────┐                           │
│   │ You: Write spec in plain English        │                           │
│   │ Claude Web: Builds quick prototype      │                           │
│   │ You: Validate it matches your vision    │                           │
│   └─────────────────────────────────────────┘                           │
│                         │                                                │
│                         ▼                                                │
│   PHASE 2: LOCAL DEVELOPMENT (Claude Code)                              │
│   ────────────────────────────────────────                               │
│   ┌─────────────────────────────────────────┐                           │
│   │ Transfer prototype to your machine      │                           │
│   │ Claude Code: Refines and extends        │                           │
│   │ You: Test locally, iterate on spec      │                           │
│   └─────────────────────────────────────────┘                           │
│                         │                                                │
│                         ▼                                                │
│   PHASE 3: PRODUCTION BUILD (AI Agent Team)                             │
│   ─────────────────────────────────────────                              │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                    │
│   │  DEV AGENT  │─►│  QA AGENT   │─►│ DOCS AGENT  │                    │
│   │             │  │             │  │             │                    │
│   │ Writes code │  │ Tests it    │  │ Documents   │                    │
│   │ from spec   │  │ thoroughly  │  │ everything  │                    │
│   └─────────────┘  └─────────────┘  └─────────────┘                    │
│                         │                                                │
│                         ▼                                                │
│   ┌─────────────────────────────────────────┐                           │
│   │  YOUR PRODUCTION APP                    │                           │
│   │     Live on the internet                │                           │
│   │     Ready for users                     │                           │
│   └─────────────────────────────────────────┘                           │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Why This Progression?

| Phase | Tool | Why |
|-------|------|-----|
| **Prototype** | Claude Web | Zero setup, instant feedback, validate ideas fast |
| **Local Dev** | Claude Code | Full file access, larger context, real development environment |
| **Production** | Agent Team | Specialized agents for quality, testing, documentation |

---

## Course Modules

**Total Duration:** ~15-20 hours
**Format:** Micro-learning videos (5-15 min each) + hands-on building YOUR app
**Structure:** 10 modules, 5 lessons each = 50 lessons total

---

### Module 1: The Autobuild Way
**Duration:** 1.5-2 hours | **Lessons:** 5

Understand the methodology and validate your app idea before writing a single line of spec.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 1.1 | The End of "Learn to Code" (For Business Apps) | 10 min | Concept |
| 1.2 | How AI Builds Apps From Specs | 12 min | Concept |
| 1.3 | What Kinds of Apps Can You Build? | 10 min | Examples |
| 1.4 | Is Your Idea Right for Autobuild? | 15 min | Self-Assessment |
| 1.5 | Validating Your App Idea | 15 min | Hands-on |

**Learning Outcomes:**
- [ ] Understand the Autobuild methodology
- [ ] Know what makes a good Autobuild project
- [ ] Validate YOUR app idea is a good fit
- [ ] Have a clear, one-sentence description of your app

**Your App Progress:** Validated idea ready for spec writing

---

### Module 2: Writing Your Spec
**Duration:** 1.5-2 hours | **Lessons:** 5

The spec is your main deliverable. Learn to write one that AI agents can build from.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 2.1 | The Autobuild Spec Template (Your Main Tool) | 15 min | Walkthrough |
| 2.2 | Section 1: App Overview and Users | 12 min | Hands-on |
| 2.3 | Section 2: Features and User Stories | 15 min | Hands-on |
| 2.4 | Section 3: Data and Business Rules | 18 min | Hands-on |
| 2.5 | Section 4: Success Criteria + Common Mistakes | 12 min | Hands-on |

**Learning Outcomes:**
- [ ] Understand each section of the spec template
- [ ] Complete the full spec FOR YOUR APP
- [ ] Define clear success criteria
- [ ] Avoid common spec-writing mistakes

**Your App Progress:** Complete spec document ready for prototyping

**Reference:** Compare your spec to the Task Tracker spec

---

### Module 3: Prototype with Claude Web
**Duration:** 1.5-2 hours | **Lessons:** 5

Get instant results. Build a working prototype in your browser with zero setup.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 3.1 | Why Start With a Prototype? | 10 min | Concept |
| 3.2 | Claude Web: Your Instant Prototyping Tool | 12 min | Demo |
| 3.3 | Feeding Your Spec to Claude | 15 min | Hands-on |
| 3.4 | Iterating on Your Prototype | 15 min | Hands-on |
| 3.5 | Understanding Context Windows and Token Limits | 12 min | Concept |

**Learning Outcomes:**
- [ ] Use Claude Web to build a prototype
- [ ] Feed your spec effectively to Claude
- [ ] Iterate based on what you see
- [ ] Understand why context windows matter

**Your App Progress:** Working prototype visible in Claude Web

**Key Concepts Introduced:**
- **Context Window:** How much the AI can "remember" in one conversation
- **Token Limits:** Why long conversations lose context

---

### Module 4: Local Development with Claude Code
**Duration:** 1.5-2 hours | **Lessons:** 5

Move from browser to your machine. Get full file access and real development power.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 4.1 | When Claude Web Hits Its Limits | 10 min | Concept |
| 4.2 | Setting Up Claude Code on Your Machine | 20 min | Hands-on |
| 4.3 | Transferring Your Prototype | 15 min | Hands-on |
| 4.4 | Running Your App Locally | 12 min | Hands-on |
| 4.5 | Local Dev vs. Cloud: Why This Matters | 10 min | Concept |

**Learning Outcomes:**
- [ ] Install and configure Claude Code
- [ ] Transfer prototype from Claude Web
- [ ] Run your app on your local machine
- [ ] Understand the benefits of local development

**Your App Progress:** Prototype running locally on your machine

---

### Module 5: Agent Handoff
**Duration:** 1.5-2 hours | **Lessons:** 5

Your prototype works. Now hand it to specialized AI agents to build the real thing.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 5.1 | Prototype vs. Production: What's Different? | 12 min | Concept |
| 5.2 | Meet the AI Agent Team | 15 min | Explanation |
| 5.3 | Preparing Your Prototype for Handoff | 12 min | Hands-on |
| 5.4 | The Handoff: Dev Agent Takes Over | 18 min | Hands-on |
| 5.5 | What to Expect During the Build | 10 min | Expectations |

**Learning Outcomes:**
- [ ] Understand prototype vs. production differences
- [ ] Know the AI agent roles (Dev, QA, Docs)
- [ ] Prepare your prototype for agent handoff
- [ ] Successfully hand off to the Dev agent

**Your App Progress:** Agents are building your production app

**Reference:** Watch the Task Tracker agent handoff

---

### Module 6: Monitoring & Testing
**Duration:** 1.5-2 hours | **Lessons:** 5

Watch your agents work. Test their output. Course-correct when needed.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 6.1 | Why Monitor Your Agents? | 10 min | Concept |
| 6.2 | Reading Agent Logs | 12 min | Hands-on |
| 6.3 | Testing Agent-Generated Code | 15 min | Hands-on |
| 6.4 | Course Correction: When Agents Drift | 15 min | Decision Guide |
| 6.5 | The Feedback Loop: Spec → Build → Test → Refine | 12 min | Concept |

**Learning Outcomes:**
- [ ] Monitor agent activity effectively
- [ ] Test agent output before accepting
- [ ] Course-correct when needed
- [ ] Understand the iterative feedback loop

**Your App Progress:** Tested, validated agent output

**Key Concepts:**
- **Agent Monitoring:** Watching what agents do without micromanaging
- **Course Correction:** Adjusting specs when output drifts

---

### Module 7: Going Multi-Agent
**Duration:** 1.5-2 hours | **Lessons:** 5

Expand from a single Dev agent to a full agentic pipeline with QA, Docs, and Review.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 7.1 | Why Multiple Agents? | 10 min | Concept |
| 7.2 | Adding the QA Agent | 15 min | Hands-on |
| 7.3 | Adding the Docs Agent | 12 min | Hands-on |
| 7.4 | How Agents Hand Off to Each Other | 12 min | Concept |
| 7.5 | Continuous Build: Keeping Agents Running | 15 min | Setup |

**Learning Outcomes:**
- [ ] Add QA agent to your pipeline
- [ ] Add Docs agent for documentation
- [ ] Understand agent-to-agent handoffs
- [ ] Set up continuous build workflow

**Your App Progress:** Full multi-agent pipeline running

**Reference:** See the Task Tracker multi-agent setup

---

### Module 8: Production Hardening
**Duration:** 1.5-2 hours | **Lessons:** 5

Make your app secure, reliable, and ready for real users.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 8.1 | What "Production-Ready" Actually Means | 10 min | Concept |
| 8.2 | Security Basics for AI-Generated Apps | 15 min | Concept |
| 8.3 | Error Handling and Edge Cases | 15 min | Hands-on |
| 8.4 | Cost Management: Keeping AI Bills Low | 12 min | Tools |
| 8.5 | Final Review Before Deployment | 12 min | Checklist |

**Learning Outcomes:**
- [ ] Understand production-ready requirements
- [ ] Secure YOUR app for real users
- [ ] Handle errors gracefully
- [ ] Manage AI costs effectively

**Your App Progress:** Production-ready, waiting for deployment

---

### Module 9: Deployment
**Duration:** 1.5-2 hours | **Lessons:** 5

Launch your app to the world. Make it accessible to users.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 9.1 | Deployment Options: Where to Host Your App | 12 min | Overview |
| 9.2 | Deploying to Vercel (Frontend Apps) | 15 min | Hands-on |
| 9.3 | Deploying to Railway/Fly.io (Full-Stack) | 15 min | Hands-on |
| 9.4 | Deploying to AWS (Enterprise) | 15 min | Hands-on |
| 9.5 | Your App Is Live! | 8 min | Celebration |

**Learning Outcomes:**
- [ ] Choose the right deployment platform
- [ ] Deploy YOUR app successfully
- [ ] Verify your app is accessible
- [ ] Share your live URL

**Your App Progress:** YOUR app is live on the internet!

---

### Module 10: What's Next
**Duration:** 1.5-2 hours | **Lessons:** 5

Your app is deployed. Now learn to maintain it, enhance it, and plan your next project.

| Lesson | Title | Duration | Type |
|--------|-------|----------|------|
| 10.1 | Post-Launch Monitoring and Maintenance | 12 min | Concept |
| 10.2 | Gathering User Feedback | 10 min | Process |
| 10.3 | Iterating on Your Live App | 15 min | Hands-on |
| 10.4 | Adding Advanced Features (APIs, Auth, AI) | 15 min | Overview |
| 10.5 | Planning Your Next Autobuild Project | 12 min | Reflection |

**Learning Outcomes:**
- [ ] Monitor your deployed app
- [ ] Collect and act on user feedback
- [ ] Plan and execute updates
- [ ] Know how to add advanced features
- [ ] Plan your next project

**Your App Progress:** Live app with a maintenance plan + ideas for what's next

---

## Spec Templates

The spec templates are the core deliverable of this course. They bridge business thinking and AI code generation.

### Template Hierarchy

| Template | Complexity | Best For |
|----------|------------|----------|
| **spec-template-simple.md** | Low | First-time builders, simple tools |
| **spec-template.md** | Medium | Most business applications |
| **spec-template-advanced.md** | High | Complex apps, integrations, multi-user |

### Template Structure

The main spec template includes these sections:

1. **App Overview** — What does it do, in one paragraph
2. **Users** — Who uses it, what roles exist
3. **Features** — What can users do (in business terms)
4. **Data** — What information gets stored
5. **Business Rules** — Logic, constraints, workflows
6. **Success Criteria** — How you know it's working
7. **Non-Goals** — What this app explicitly won't do

### Reference Example Specs

The course includes complete, working example specs you can reference:

- **Task Tracker** — Simple personal task management (primary reference)
- **Booking System** — Appointment scheduling with calendar
- **Client Portal** — Client-facing project/invoice viewer
- **Dashboard** — KPI tracking and visualization

Use these to understand the spec format, not as apps to build.

---

## App Ideas That Work Well

If you're not sure what to build, here are proven patterns:

### Internal Tools
- Team task/project tracker
- Approval workflow system
- Inventory tracker
- Meeting scheduler

### Customer-Facing
- Booking/appointment system
- Client portal (view projects/invoices)
- Simple marketplace or directory
- Feedback/survey collector

### Data/Reporting
- KPI dashboard
- Report generator
- Data entry forms
- Simple CRM

### The Best Idea?
**Something YOU actually need.** If you'll use it, you'll finish it.

---

## Resources

### Included Materials

| Resource | Description |
|----------|-------------|
| **Glossary** | Terms and definitions used in the course |
| **Reading List** | Recommended articles, books, videos |
| **Tools Comparison** | When to use which AI tool/platform |

### Cheatsheets

Quick reference guides for:

- **Spec Writing** — Patterns for clear, AI-friendly specs
- **AI Prompting** — How to communicate with AI agents effectively
- **Deployment** — Quick reference for common deployment platforms

### Community

- **GitHub Discussions** — Q&A, show and tell, announcements
- **Module-specific Q&A** — Get help with specific lessons
- **App Showcase** — Share YOUR completed app

---

## Course Access

This course is **completely free and open source**.

- **Content License:** CC BY 4.0 (share and adapt with attribution)
- **Code License:** MIT (use however you want)

No sign-up required. No paywall. No upsells.

---

## Document Metadata

```yaml
Document: Autobuild.ai Course Content
Purpose: Student-facing course structure and learning path
Version: 5.0
Created: 2025
Approach: Build YOUR app throughout (not follow-along)
Progression: Claude Web (prototype) → Claude Code (local) → Agents (production)
Structure: 10 modules × 5 lessons = 50 total lessons
New in v5: Split into 10 micro-learning modules, removed capstone
```

---

**Ready to start? Bring your app idea to Module 1: The Autobuild Way.**
