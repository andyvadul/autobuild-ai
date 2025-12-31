# Claude Code Best Practices

This is a summary from a talk by **Cal**, a core contributor on the Claude Code team at Anthropic, covering how Claude Code works and best practices for using it effectively.

## What is Claude Code?

Claude Code is like having a terminal-expert coworker beside you at all times. It's a "pure agent" consisting of:
- **Instructions + powerful tools** running in a loop until the task is complete
- **Tools**: file creation/editing, terminal commands, MCP integrations
- **Agentic search**: No indexing or RAG - Claude explores codebases using tools like `glob`, `grep`, and `find`, just like a human developer would

## Good Use Cases

1. **Discovery** - Onboarding to new codebases, understanding git history, finding features
2. **Planning** - Use Claude as a thought partner before implementing (ask for 2-3 options)
3. **Building** - Zero-to-one projects and working in existing codebases
4. **Testing** - Easy to add unit tests, resulting in high test coverage
5. **Git workflows** - Auto-generate commits and PR messages
6. **Migrations** - Large refactoring projects (e.g., PHP to React, Java version upgrades)
7. **CLI mastery** - Git, Docker, BigQuery, fixing messy rebases

## Best Practices

| Practice | Details |
|----------|---------|
| **Use `claude.md` files** | Add project context, style guides, test commands, project layout. Can be per-project or in home directory |
| **Permission management** | Use `Shift+Tab` for auto-accept mode; configure always-approved commands (e.g., `npm run test`) |
| **CLI integrations** | Prefer well-documented CLI tools (like `gh`) over MCP servers |
| **Context management** | Use `/clear` to start fresh or `/compact` to summarize and continue |
| **Planning & todos** | Ask Claude to search and propose a plan before implementing; watch the todo list for wrong paths |
| **Test-driven development** | Small changes → run tests → check TypeScript/linting → commit regularly |
| **Use screenshots** | Claude is multimodal - paste images or reference mock files |

## Advanced Techniques

- **Run multiple Claude instances** (2-4 in tmux/tabs) and orchestrate them
- **Press Escape** to interrupt and redirect Claude; **double-escape** to jump back in conversation history
- **MCP servers** for capabilities beyond bash
- **Headless automation** via the SDK (CI/CD, GitHub Actions)

## Recent Features

- `/model` command to switch between Sonnet and Opus
- **"Think hard"** prompting now works *between* tool calls (Claude 4+)
- VS Code and JetBrains integrations with file awareness
- Use `@` syntax in `claude.md` to reference other files

## Multi-Agent Workflows

For parallel agents that need to share context, have them write to a shared markdown file (e.g., `ticket.md`) that other agents can read.

---

# Claude Code: 36 Tips from Beginner to Master

*Summary from Avthar's comprehensive Claude Code tutorial video.*

## Level 1: Beginner (Foundations)

### Installation Options
1. **Local installation** - Install via terminal on your laptop (most common)
2. **Remote server** - Install on AWS/DigitalOcean/Hetzner for backend work and coding from anywhere (e.g., via Termius on iOS)
3. **IDE integration** - Use inside Cursor, Windsurf, or VS Code

### Essential Features

| Feature | How to Use |
|---------|------------|
| **To-do lists** | Claude auto-creates them, or explicitly ask for one. Watch items get checked off as Claude works |
| **Bash mode** | Run bash commands inside Claude Code without exiting |
| **Instant documentation** | Ask Claude to explain architecture and save to `architecture.md` |
| **Auto-accept mode** | Press `Shift+Tab` to let Claude work without permission prompts |
| **Model switching** | Use `/model` - Opus for tough problems, Sonnet for routine tasks |
| **Interrupt** | Press `Escape` once to stop, twice to go back to previous prompt |
| **Message queue** | Type while Claude is working; messages queue up for later |
| **Long prompts** | Put prompts in a markdown file, reference with `@filename.md` |

### Debugging
- **Screenshot method** - Paste UI screenshots for visual context
- **Let Claude write tests** - Focus on end-to-end tests, not implementation-specific ones
- **Test-driven development** - Ask Claude to write tests first, then implement

### The claude.md File (Most Important!)

Your project's memory - added to context every session. Include:
- Git workflows and best practices
- Project/architecture overview
- Build commands
- Testing and debugging practices
- Documentation how-tos

**Pro tip**: Ask Claude to write and update your `claude.md` file for you.

---

## Level 2: Intermediate (Workflow Enhancements)

### Planning & Thinking

| Mode | Usage |
|------|-------|
| **Plan mode** | Press `Tab+Shift` until "plan only mode" appears - review before coding |
| **Opus plan mode** | Opus for planning, Sonnet for implementation (via `/model`) |
| **Think keywords** | `think` (basic), `think hard` (deeper), `ultra think` (maximum) |
| **Parallel subagents** | Ask Claude to explore multiple solutions simultaneously |

### Beyond Code

- **Web research** - Claude can search the web and read websites
- **PDF reading** - Combine PDF content with web searches
- **Document generation** - PRDs, UX guides, API docs, technical design docs
- **Change tracking** - Changelogs, decision docs, feature documentation

### GitHub Integration

Run `/install-gh-actions` to enable:
- Tag `@claude` in issues/PRs to get fixes
- Claude runs via GitHub Actions (no local machine needed)
- Automatic PR reviews

### Mindset for Success

**Think like a product manager:**
1. Give Claude clear context and constraints
2. Verify outputs at higher abstraction levels (does the app work? do tests pass?)
3. You don't need to understand every line of code

---

## Level 3: Master (Advanced Techniques)

### Multi-Claude with Git Worktrees

Work on multiple features simultaneously without conflicts:

```bash
# Create worktrees
mkdir .trees
git worktree add .trees/feature-a feature-a
git worktree add .trees/feature-b feature-b

# Run Claude in each worktree (separate terminals)
cd .trees/feature-a && claude
cd .trees/feature-b && claude

# Merge when done
git worktree remove .trees/feature-a
```

### Custom Slash Commands

Create shortcuts for repetitive prompts:

1. Create `.claude/commands/` folder
2. Add markdown files (e.g., `changelog.md`)
3. Include: description, allowed tools, command prompt

Commands can be **project-specific** or **personal** (applies to all projects).

### Custom Subagents

Specialized AI assistants for specific domains:
- Use `/agents` command to create via wizard
- Examples: UX design, API design, security review, database admin
- Each has custom tools and system prompts
- Claude auto-delegates to relevant subagents

### MCP Servers

Extend Claude's capabilities to third-party tools:
- **Database MCPs** - MongoDB, Postgres, Supabase
- **Playwright MCP** - Browser automation and visual testing
- **Figma MCP** - Design to code

---

## Pricing

| Plan | Cost | Notes |
|------|------|-------|
| Pro | $20/mo | Good for getting started |
| Max 5X | $100/mo | 5x rate limits vs Pro |
| Max 20X | $200/mo | 20x rate limits (recommended for serious use) |
| API | Variable | Expensive; only recommended if company pays |

---

# Long-Running Agents: Effective Harnesses

*Summary from Anthropic's engineering blog: [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)*

## The Problem

Long-running agents struggle when tasks span multiple context windows. Each new session starts with **no memory** of prior work, making it difficult to maintain progress on complex projects.

## Two-Agent Architecture

### 1. Initializer Agent (First Session)

Sets up the foundational environment:
- Creates an `init.sh` script for running dev servers
- Establishes a **progress tracking file** documenting agent work
- Makes initial git commits establishing baseline state

### 2. Coding Agent (Subsequent Sessions)

Focuses on incremental progress:
- Reads progress logs and git history to understand context
- Implements **one feature at a time** (not comprehensive solutions)
- Commits changes with descriptive messages
- Leaves codebase in a "clean state" suitable for merging

## Key Patterns

### Feature List File (JSON Format)

Maintain a comprehensive feature registry with status tracking:

```json
{
  "features": [
    {"id": 1, "name": "Search box UI", "status": "complete"},
    {"id": 2, "name": "AJAX results", "status": "in_progress"},
    {"id": 3, "name": "Filters panel", "status": "pending"}
  ]
}
```

> "It is unacceptable to remove or edit tests because this could lead to missing or buggy functionality."

Using JSON prevents the model from inappropriately modifying specifications.

### Incremental Progress Over One-Shotting

Agents tend to attempt too much at once, leaving features half-implemented. **Constrain each session to single features** - this dramatically improves consistency and prevents context exhaustion mid-implementation.

### Testing as Verification

Agents need **explicit prompting** to perform end-to-end testing. Without this, they mark features complete despite non-functional implementation. Use browser automation tools (Puppeteer/Playwright MCP) to verify.

## Session Startup Sequence

Each session should follow a structured startup:

1. Verify working directory
2. Review progress documentation
3. Consult feature list
4. Run basic functionality tests
5. **Then** start new development

## Practical Implementation

```bash
# Session 1: Initializer
claude
> "Set up progress tracking in progress.md, create feature list in features.json,
   commit baseline state"

# Session 2+: Coding Agent
claude
> "Read progress.md and features.json, pick ONE pending feature,
   implement it fully, test it, commit, update progress.md"
```

## Separation Benefits

| Benefit | Why |
|---------|-----|
| **Better reasoning** | Planner focuses on strategy, executor on implementation |
| **Improved reliability** | Each agent has clear, focused responsibility |
| **Easier debugging** | Inspect plans before execution |
| **Resource efficiency** | Use different models for planning vs coding |
| **Fresh perspective** | Second agent catches issues first might miss |

## Related: Planner/Executor Pattern

From [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices):

> "Use one Claude to write code; use another Claude to verify. This separation often yields better results than having a single Claude handle everything."

Methods:
- Run `/clear` then review in same terminal
- Start second Claude in new terminal
- Use git worktrees for complete isolation
