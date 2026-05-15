# Claude Code Plugins

These are the plugins active in my setup — organized by what problem they solve, not alphabetically.

Install any of them with:

```bash
claude plugin install <name>
```

---

## 🏗 Foundations — install these first

| Plugin | What it does |
|--------|-------------|
| `superpowers` | Core skills library: TDD, systematic debugging, git worktrees, writing plans, dispatching parallel agents. The foundation everything else builds on. |
| `remember` | Continuous memory across sessions. Compresses conversations into structured memory files so Claude remembers your preferences and project context between restarts. |
| `commit-commands` | Adds `/commit` and `/commit-push-pr` slash commands. Handles staging, commit message, push, and PR creation in one shot. |
| `hookify` | Analyzes your conversation and turns patterns of unwanted behavior into hooks. `/hookify` with no args looks back at the session and suggests rules to prevent recurring mistakes. |

```bash
claude plugin install superpowers remember commit-commands hookify
```

---

## 📝 Code Quality

| Plugin | What it does |
|--------|-------------|
| `code-review` | Multi-agent PR code review. Launches specialist agents in parallel for style, logic, and security — then filters to only high-confidence findings. |
| `pr-review-toolkit` | Deeper PR review suite with separate agents for: comment accuracy, test coverage, silent failures/error handling, type design, and code simplicity. |
| `code-simplifier` | After you finish a feature, `/simplify` reviews the changed code for reuse, clarity, and quality — then fixes what it finds. |
| `feature-dev` | Full feature development workflow: codebase explorer → architect → implementer → reviewer, all coordinated. Use for non-trivial features. |

```bash
claude plugin install code-review pr-review-toolkit code-simplifier feature-dev
```

---

## 🌐 Browser & UI

| Plugin | What it does |
|--------|-------------|
| `playwright` | Microsoft's Playwright MCP server. Claude can open browsers, click, fill forms, take screenshots, and run assertions directly. |
| `chrome-devtools-mcp` | Chrome DevTools MCP from the official Chrome team. Deeper than Playwright — console logs, network requests, performance traces, memory snapshots, accessibility audits. |
| `frontend-design` | Design-first UI skill. Generates distinctive, production-grade interfaces — avoids generic AI aesthetics. |

```bash
# playwright and frontend-design are from the official marketplace
claude plugin install playwright frontend-design

# chrome-devtools-mcp is from the Chrome team's own marketplace
claude plugin install chrome-devtools-mcp@chrome-devtools-plugins
```

---

## 🔗 Integrations

| Plugin | What it does |
|--------|-------------|
| `github` | Official GitHub MCP. Create issues, manage PRs, search code, review comments — without leaving Claude. |
| `slack` | Slack MCP + skills for searching messages, sending updates, channel digests, and drafting announcements. |
| `vercel` | Full Vercel workflow: deploy, manage env vars, browse marketplace integrations, tail logs. |
| `neon` | Neon Postgres MCP. Manage projects, branches, and databases; run queries from within Claude. |
| `context7` | Upstash Context7 — pulls current, version-specific library docs on demand. Eliminates stale API hallucinations. |

```bash
claude plugin install github slack vercel neon context7
```

---

## 🛠 Language & Framework

| Plugin | What it does |
|--------|-------------|
| `laravel-boost` | Laravel MCP toolkit — intelligent assistance for Artisan, Eloquent, Blade, routes, and migrations. |
| `php-lsp` | PHP language server. Gives Claude real-time type info, go-to-definition, and diagnostics in PHP projects. |
| `typescript-lsp` | TypeScript language server. Same as above for TS — especially useful in large codebases where types span many files. |
| `agent-sdk-dev` | Claude Agent SDK development plugin — skills and agents for building, scaffolding, and verifying SDK apps. |

```bash
claude plugin install laravel-boost php-lsp typescript-lsp agent-sdk-dev
```

---

## ⚙️ Meta — build and extend Claude Code itself

| Plugin | What it does |
|--------|-------------|
| `plugin-dev` | Toolkit for building plugins. Skills for creating agents, commands, hooks, and MCP integrations with proper structure. |
| `skill-creator` | Create new skills, improve existing ones, run evals to measure performance. |
| `claude-md-management` | Audits and improves `CLAUDE.md` files. `/revise-claude-md` captures session learnings and writes them back. |
| `claude-code-setup` | Analyzes any codebase and recommends tailored Claude Code automations — hooks, skills, MCPs, agents. Great first thing to run on a new project. |
| `learning-output-style` | Changes Claude's output style to interactive teaching mode — requests your input at decision points, explains tradeoffs, adds educational insights. (What you're seeing in this session.) |
| `playground` | `/playground <topic>` generates a self-contained interactive HTML explorer with live controls and preview. |
| `ralph-loop` | Continuous self-referential improvement loops. Claude re-evaluates and iterates its own output until a quality bar is met. |
| `notifier` | Push notification sounds when long tasks complete. Never miss a finished build while you're in another tab. Requires adding a custom marketplace first (see below). |

```bash
# Most of these are in the official marketplace
claude plugin install plugin-dev skill-creator claude-md-management claude-code-setup learning-output-style playground ralph-loop

# Notifier is in a separate marketplace
claude plugin marketplace add convocli-notifier github:convocli/notifier
claude plugin install notifier@convocli-notifier
```

---

## Installed but currently off

These are installed but disabled — either situational or still being evaluated:

| Plugin | Why it's off |
|--------|-------------|
| `serena` | Semantic code analysis MCP — powerful but heavy; I enable it per-project |
| `ralph-wiggum` | Predecessor to `ralph-loop`; keeping for comparison |
| `convosync` | Conversation sync tool — paused while evaluating workflow fit |
| `greptile` | AI PR review via Greptile — overlaps with `code-review` |
| `linear` | Linear issue tracking — not on a Linear team right now |
| `semgrep` | Security scanning for agent-generated code — worth enabling if shipping to prod |
| `security-guidance` | Hook-based security reminders when editing files |
| `mcp-server-dev` | MCP server building skills — use when building an MCP, not always |

---

## How the plugin system works

Plugins live in `~/.claude/plugins/`. Each one can contribute any combination of:
- **Skills** — instructions loaded into context when triggered
- **Agents** — specialized subagents with their own system prompts and tool access  
- **Commands** — slash commands like `/commit` or `/hookify`
- **Hooks** — shell commands that run on Claude Code events (PreToolUse, PostToolUse, Stop, etc.)
- **MCP servers** — external tool servers that give Claude new capabilities

The official marketplace is `anthropics/claude-plugins-official` on GitHub. Anyone can publish a plugin by hosting a `marketplace.json` and pointing Claude at it.
