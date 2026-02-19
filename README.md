# drixxodev-ai

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Node](https://img.shields.io/badge/node-%3E%3D18-brightgreen)
![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white)
![Go](https://img.shields.io/badge/-Go-00ADD8?logo=go&logoColor=white)
![Java](https://img.shields.io/badge/-Java-ED8B00?logo=openjdk&logoColor=white)
![Shell](https://img.shields.io/badge/-Shell-4EAA25?logo=gnu-bash&logoColor=white)

> **982 skills** | **13 agents** | **31 commands** | **23 rules** | **15 MCP servers** | **6 languages supported**

A comprehensive, production-ready collection of Claude Code configurations -- agents, skills, hooks, commands, rules, and MCP server configs built for real-world AI-assisted development workflows.

---

## Table of Contents

- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Agents (13)](#agents)
- [Commands (31)](#commands)
- [Skills](#skills)
  - [Core Development Skills (74)](#core-development-skills)
  - [Service Automation Skills (908)](#service-automation-skills)
- [Rules (23)](#rules)
- [Hooks (14)](#hooks)
- [Contexts (3)](#contexts)
- [MCP Server Configs (15)](#mcp-server-configs)
- [Scripts](#scripts)
- [Schemas](#schemas)
- [Examples](#examples)
- [Installation](#installation)
- [Running Tests](#running-tests)
- [Cross-Platform Support](#cross-platform-support)
- [Token Optimization](#token-optimization)
- [Contributing](#contributing)
- [License](#license)

---

## Quick Start

```bash
# Clone the repo
git clone https://github.com/drixxodev/drixxodev-ai.git
cd drixxodev-ai

# Install dependencies
npm install

# Install rules for your language(s)
./install.sh typescript    # or python, golang
# Multiple languages:
# ./install.sh typescript python golang
```

---

## Project Structure

```
drixxodev-ai/
├── agents/           # 13 specialized subagents
├── commands/         # 31 slash commands
├── skills/           # 982 skills (74 core + 908 automation)
├── rules/            # 23 rules across 4 categories
├── hooks/            # 14 hook configurations
├── contexts/         # 3 dynamic context modes
├── scripts/          # Cross-platform Node.js scripts
├── schemas/          # JSON schemas for validation
├── examples/         # Example CLAUDE.md configs
├── mcp-configs/      # 15 MCP server configurations
├── docs/             # Translations (ja-JP, zh-CN, zh-TW)
├── tests/            # Test suite
├── index.js          # Package entry point
├── install.sh        # Installation wizard
└── package.json
```

---

## Agents

13 specialized subagents that handle delegated tasks with limited scope. Located in `agents/`.

| Agent | File | Description |
|-------|------|-------------|
| Planner | `planner.md` | Feature implementation planning and task decomposition |
| Architect | `architect.md` | System design decisions and architecture guidance |
| TDD Guide | `tdd-guide.md` | Test-driven development enforcement and workflow |
| Code Reviewer | `code-reviewer.md` | Code quality, security, and maintainability review |
| Security Reviewer | `security-reviewer.md` | Vulnerability analysis and OWASP Top 10 auditing |
| Build Error Resolver | `build-error-resolver.md` | Diagnose and fix build errors |
| E2E Runner | `e2e-runner.md` | Playwright end-to-end test generation and execution |
| Refactor Cleaner | `refactor-cleaner.md` | Dead code detection and cleanup |
| Doc Updater | `doc-updater.md` | Documentation sync and maintenance |
| Go Reviewer | `go-reviewer.md` | Go-specific code review |
| Go Build Resolver | `go-build-resolver.md` | Go build error resolution |
| Python Reviewer | `python-reviewer.md` | Python code review (PEP 8, type hints, security) |
| Database Reviewer | `database-reviewer.md` | Database schema, query, and migration review |

---

## Commands

31 slash commands for quick execution. Located in `commands/`.

### Planning & Architecture

| Command | File | Description |
|---------|------|-------------|
| `/plan` | `plan.md` | Create an implementation plan for a feature |
| `/orchestrate` | `orchestrate.md` | Multi-agent coordination and workflow |

### Testing & Quality

| Command | File | Description |
|---------|------|-------------|
| `/tdd` | `tdd.md` | Enforce test-driven development workflow |
| `/e2e` | `e2e.md` | Generate end-to-end tests |
| `/test-coverage` | `test-coverage.md` | Analyze test coverage |
| `/code-review` | `code-review.md` | Run code quality review |
| `/verify` | `verify.md` | Run verification loop |
| `/eval` | `eval.md` | Evaluate code against criteria |
| `/checkpoint` | `checkpoint.md` | Save verification state |

### Build & Fix

| Command | File | Description |
|---------|------|-------------|
| `/build-fix` | `build-fix.md` | Fix build errors automatically |
| `/refactor-clean` | `refactor-clean.md` | Remove dead code and clean up |

### Go-Specific

| Command | File | Description |
|---------|------|-------------|
| `/go-review` | `go-review.md` | Go code review |
| `/go-test` | `go-test.md` | Go TDD workflow |
| `/go-build` | `go-build.md` | Fix Go build errors |

### Python-Specific

| Command | File | Description |
|---------|------|-------------|
| `/python-review` | `python-review.md` | Python code review |

### Learning & Instincts

| Command | File | Description |
|---------|------|-------------|
| `/learn` | `learn.md` | Extract patterns mid-session |
| `/instinct-status` | `instinct-status.md` | View learned instincts with confidence scores |
| `/instinct-import` | `instinct-import.md` | Import instincts from files |
| `/instinct-export` | `instinct-export.md` | Export instincts for sharing |
| `/evolve` | `evolve.md` | Cluster related instincts into skills |
| `/skill-create` | `skill-create.md` | Generate skills from git history |

### Multi-Agent Orchestration

| Command | File | Description |
|---------|------|-------------|
| `/multi-plan` | `multi-plan.md` | Multi-agent task decomposition |
| `/multi-execute` | `multi-execute.md` | Orchestrated multi-agent workflows |
| `/multi-backend` | `multi-backend.md` | Backend multi-service orchestration |
| `/multi-frontend` | `multi-frontend.md` | Frontend multi-service orchestration |
| `/multi-workflow` | `multi-workflow.md` | General multi-service workflows |

### Utilities

| Command | File | Description |
|---------|------|-------------|
| `/pm2` | `pm2.md` | PM2 service lifecycle management |
| `/sessions` | `sessions.md` | Session history management |
| `/update-docs` | `update-docs.md` | Update project documentation |
| `/update-codemaps` | `update-codemaps.md` | Update codemaps |
| `/setup-pm` | `setup-pm.md` | Configure package manager |

---

## Skills

982 total skills located in `skills/`. Broken into two categories:

### Core Development Skills

74 skills covering development patterns, testing, security, and tooling.

#### Language & Framework Patterns

| Skill | Description |
|-------|-------------|
| `coding-standards` | Language-agnostic best practices |
| `backend-patterns` | API, database, and caching patterns |
| `frontend-patterns` | React, Next.js, and frontend patterns |
| `python-patterns` | Python idioms and best practices |
| `golang-patterns` | Go idioms and best practices |
| `django-patterns` | Django models, views, and patterns |
| `springboot-patterns` | Java Spring Boot patterns |
| `jpa-patterns` | JPA/Hibernate patterns |
| `java-coding-standards` | Java coding standards |
| `cpp-coding-standards` | C++ coding standards (Core Guidelines) |
| `swift-actor-persistence` | Thread-safe Swift data persistence with actors |
| `swift-protocol-di-testing` | Protocol-based dependency injection for testable Swift |
| `postgres-patterns` | PostgreSQL optimization patterns |
| `clickhouse-io` | ClickHouse analytics, queries, and data engineering |

#### Testing

| Skill | Description |
|-------|-------------|
| `tdd-workflow` | TDD methodology (RED/GREEN/REFACTOR) |
| `python-testing` | Python testing with pytest |
| `golang-testing` | Go testing, TDD, and benchmarks |
| `cpp-testing` | C++ testing with GoogleTest, CMake/CTest |
| `django-tdd` | Django TDD workflow |
| `springboot-tdd` | Spring Boot TDD |
| `e2e-testing` | Playwright E2E patterns and Page Object Model |
| `webapp-testing` | Web application testing patterns |

#### Security

| Skill | Description |
|-------|-------------|
| `security-review` | Security checklist with cloud infrastructure review |
| `security-scan` | AgentShield security auditor integration |
| `django-security` | Django security best practices |
| `springboot-security` | Spring Boot security |

#### Verification & Evaluation

| Skill | Description |
|-------|-------------|
| `verification-loop` | Continuous verification patterns |
| `eval-harness` | Verification loop evaluation |
| `django-verification` | Django verification loops |
| `springboot-verification` | Spring Boot verification |

#### DevOps & Deployment

| Skill | Description |
|-------|-------------|
| `deployment-patterns` | CI/CD, Docker, health checks, rollbacks |
| `docker-patterns` | Docker Compose, networking, volumes, security |
| `database-migrations` | Migration patterns (Prisma, Drizzle, Django, Go) |
| `api-design` | REST API design, pagination, error responses |

#### Learning & Context Management

| Skill | Description |
|-------|-------------|
| `continuous-learning` | Auto-extract patterns from sessions (v1) |
| `continuous-learning-v2` | Instinct-based learning with confidence scoring |
| `iterative-retrieval` | Progressive context refinement for subagents |
| `strategic-compact` | Manual compaction suggestions at logical breakpoints |
| `configure-ecc` | Interactive installation wizard |

#### AI & LLM Patterns

| Skill | Description |
|-------|-------------|
| `cost-aware-llm-pipeline` | LLM cost optimization, model routing, budget tracking |
| `regex-vs-llm-structured-text` | Decision framework: regex vs LLM for text parsing |
| `content-hash-cache-pattern` | SHA-256 content hash caching for file processing |

#### Productivity & Utilities

| Skill | Description |
|-------|-------------|
| `artifacts-builder` | Build and manage artifacts |
| `brand-guidelines` | Brand guidelines management |
| `canvas-design` | Canvas design patterns |
| `changelog-generator` | Generate changelogs automatically |
| `competitive-ads-extractor` | Extract competitive advertising data |
| `composio-sdk` | Composio SDK integration |
| `connect` | Connection management |
| `connect-apps` | App connection patterns |
| `connect-apps-plugin` | Plugin connection patterns |
| `content-research-writer` | Content research and writing |
| `developer-growth-analysis` | Developer growth analytics |
| `document-skills` | Document processing skills |
| `domain-name-brainstormer` | Domain name brainstorming |
| `file-organizer` | File organization automation |
| `image-enhancer` | Image enhancement |
| `internal-comms` | Internal communications |
| `invoice-organizer` | Invoice organization |
| `langsmith-fetch` | LangSmith data fetching |
| `lead-research-assistant` | Lead research automation |
| `mcp-builder` | MCP server builder |
| `meeting-insights-analyzer` | Meeting insights analysis |
| `nutrient-document-processing` | Document processing with Nutrient API |
| `raffle-winner-picker` | Raffle winner selection |
| `skill-creator` | Skill creation from git history |
| `skill-share` | Skill sharing utilities |
| `slack-gif-creator` | Slack GIF creation |
| `tailored-resume-generator` | Resume generation |
| `template-skill` | Template for creating new skills |
| `theme-factory` | Theme creation |
| `twitter-algorithm-optimizer` | Twitter algorithm optimization |
| `video-downloader` | Video downloading |
| `project-guidelines-example` | Template for project-specific skills |

### Service Automation Skills

908 service automation skills for integrating with third-party APIs and platforms. Each follows the `*-automation` naming convention and provides ready-to-use integration patterns.

**Categories include:**

- **CRM & Sales**: Salesforce, HubSpot, Pipedrive, Close, Attio, and 50+ more
- **Communication**: Slack, Discord, Telegram, WhatsApp, Twitch, and 30+ more
- **Project Management**: Jira, Asana, Monday, Linear, Trello, ClickUp, and 20+ more
- **Cloud & DevOps**: AWS, Cloudflare, Vercel, Railway, Docker Hub, Render, and 20+ more
- **Marketing & Email**: Mailchimp, SendGrid, Brevo, ConvertKit, and 40+ more
- **Analytics**: Amplitude, Mixpanel, PostHog, Google Analytics, and 15+ more
- **AI/ML**: OpenAI, Anthropic, Replicate, Mistral, Groq, and 15+ more
- **Databases**: Supabase, Airtable, Baserow, Snowflake, InfluxDB, and 10+ more
- **Payments**: Stripe, Braintree, Square, LemonSqueezy, Gumroad, and 10+ more
- **File & Storage**: Dropbox, Box, Google Drive, OneDrive, Cloudinary, and 10+ more
- **Authentication**: Auth0, Firebase, Clerk, and more
- **And hundreds more** covering virtually every major SaaS platform

---

## Rules

23 always-follow guidelines organized by scope. Located in `rules/`.

### Common Rules (language-agnostic) -- `rules/common/`

| Rule | File | Description |
|------|------|-------------|
| Coding Style | `coding-style.md` | Immutability, file organization, naming conventions |
| Git Workflow | `git-workflow.md` | Commit format, PR process, branch strategy |
| Testing | `testing.md` | TDD enforcement, 80% coverage requirement |
| Performance | `performance.md` | Model selection, context management |
| Patterns | `patterns.md` | Design patterns, skeleton projects |
| Hooks | `hooks.md` | Hook architecture, TodoWrite patterns |
| Agents | `agents.md` | When and how to delegate to subagents |
| Security | `security.md` | Mandatory security checks |

### TypeScript Rules -- `rules/typescript/`

| Rule | File | Description |
|------|------|-------------|
| Coding Style | `coding-style.md` | TS/JS specific style and conventions |
| Hooks | `hooks.md` | TypeScript hook patterns |
| Patterns | `patterns.md` | TypeScript design patterns |
| Security | `security.md` | TypeScript security practices |
| Testing | `testing.md` | TypeScript testing patterns |

### Python Rules -- `rules/python/`

| Rule | File | Description |
|------|------|-------------|
| Coding Style | `coding-style.md` | PEP 8, type hints, Pythonic conventions |
| Hooks | `hooks.md` | Python hook patterns |
| Patterns | `patterns.md` | Python design patterns |
| Security | `security.md` | Python security practices |
| Testing | `testing.md` | pytest patterns and conventions |

### Go Rules -- `rules/golang/`

| Rule | File | Description |
|------|------|-------------|
| Coding Style | `coding-style.md` | Go idioms and formatting |
| Hooks | `hooks.md` | Go hook patterns |
| Patterns | `patterns.md` | Go design patterns |
| Security | `security.md` | Go security practices |
| Testing | `testing.md` | Go testing patterns |

---

## Hooks

14 hook configurations across 6 lifecycle phases. Defined in `hooks/hooks.json`.

### PreToolUse (5 hooks)

| Hook | Description |
|------|-------------|
| Block dev server outside tmux | Prevents `npm run dev` etc. outside tmux for log access |
| Tmux reminder | Suggests tmux for long-running commands |
| Git push reminder | Reminds to review changes before `git push` |
| Block random .md files | Prevents unnecessary documentation file creation |
| Suggest compaction | Suggests `/compact` at logical intervals |

### PostToolUse (4 hooks)

| Hook | Description |
|------|-------------|
| PR URL logger | Logs PR URL and review command after `gh pr create` |
| Build analysis | Async background analysis after build commands |
| Auto-format | Runs Prettier on JS/TS files after edits |
| TypeScript check | Runs `tsc` on `.ts/.tsx` files after edits |
| Console.log warning | Warns about `console.log` statements after edits |

### PreCompact (1 hook)

| Hook | Description |
|------|-------------|
| Save state | Preserves session state before context compaction |

### SessionStart (1 hook)

| Hook | Description |
|------|-------------|
| Load context | Loads previous context and detects package manager |

### Stop (1 hook)

| Hook | Description |
|------|-------------|
| Console.log check | Checks for `console.log` in modified files after each response |

### SessionEnd (2 hooks)

| Hook | Description |
|------|-------------|
| Persist state | Saves session state on end |
| Evaluate session | Extracts patterns from the session for learning |

---

## Contexts

3 dynamic system prompt injection contexts. Located in `contexts/`.

| Context | File | Description |
|---------|------|-------------|
| Development | `dev.md` | Development mode -- coding, building, testing |
| Review | `review.md` | Code review mode -- quality, security, best practices |
| Research | `research.md` | Research/exploration mode -- investigation, analysis |

---

## MCP Server Configs

15 pre-configured MCP servers. Located in `mcp-configs/mcp-servers.json`.

| Server | Type | Description |
|--------|------|-------------|
| GitHub | npx | GitHub operations -- PRs, issues, repos |
| Firecrawl | npx | Web scraping and crawling |
| Supabase | npx | Supabase database operations |
| Memory | npx | Persistent memory across sessions |
| Sequential Thinking | npx | Chain-of-thought reasoning |
| Vercel | HTTP | Vercel deployments and projects |
| Railway | npx | Railway deployments |
| Cloudflare Docs | HTTP | Cloudflare documentation search |
| Cloudflare Workers Builds | HTTP | Cloudflare Workers builds |
| Cloudflare Workers Bindings | HTTP | Cloudflare Workers bindings |
| Cloudflare Observability | HTTP | Cloudflare observability/logs |
| ClickHouse | HTTP | ClickHouse analytics queries |
| Context7 | npx | Live documentation lookup |
| Magic UI | npx | Magic UI components |
| Filesystem | npx | Filesystem operations |

Copy the servers you need to your `~/.claude.json` and replace `YOUR_*_HERE` placeholders with actual API keys.

---

## Scripts

Cross-platform Node.js scripts located in `scripts/`.

### Hook Scripts (`scripts/hooks/`)

| Script | Description |
|--------|-------------|
| `session-start.js` | Load context on session start |
| `session-end.js` | Save state on session end |
| `pre-compact.js` | Pre-compaction state saving |
| `suggest-compact.js` | Strategic compaction suggestions |
| `evaluate-session.js` | Extract patterns from sessions |
| `check-console-log.js` | Check for console.log in modified files |
| `post-edit-format.js` | Auto-format after edits |
| `post-edit-typecheck.js` | TypeScript check after edits |
| `post-edit-console-warn.js` | Warn about console.log after edits |

### Library Scripts (`scripts/lib/`)

| Script | Description |
|--------|-------------|
| `utils.js` | Cross-platform file/path/system utilities |
| `package-manager.js` | Package manager detection and selection |
| `session-manager.js` | Session management utilities |
| `session-aliases.js` | Session alias utilities |

### CI Validation (`scripts/ci/`)

| Script | Description |
|--------|-------------|
| `validate-agents.js` | Validate agent definitions |
| `validate-commands.js` | Validate command definitions |
| `validate-rules.js` | Validate rule files |
| `validate-skills.js` | Validate skill definitions |
| `validate-hooks.js` | Validate hook configurations |

---

## Schemas

JSON schemas for validation. Located in `schemas/`.

| Schema | Description |
|--------|-------------|
| `hooks.schema.json` | Hook configuration validation |
| `package-manager.schema.json` | Package manager config validation |
| `plugin.schema.json` | Plugin definition validation |

---

## Examples

Example configurations and real-world setups. Located in `examples/`.

| Example | Description |
|---------|-------------|
| `CLAUDE.md` | Example project-level Claude config |
| `user-CLAUDE.md` | Example user-level Claude config |
| `saas-nextjs-CLAUDE.md` | Real-world SaaS (Next.js + Supabase + Stripe) |
| `go-microservice-CLAUDE.md` | Real-world Go microservice (gRPC + PostgreSQL) |
| `django-api-CLAUDE.md` | Real-world Django REST API (DRF + Celery) |
| `rust-api-CLAUDE.md` | Real-world Rust API (Axum + SQLx + PostgreSQL) |
| `statusline.json` | Example statusline configuration |

---

## Installation

### Option 1: npm Install

```bash
npm install drixxodev-ai
npx drixxodev-ai-install typescript   # or python, golang
```

### Option 2: Clone and Install

```bash
git clone https://github.com/drixxodev/drixxodev-ai.git
cd drixxodev-ai
npm install

# Install rules for your stack
./install.sh typescript
# Multiple languages:
./install.sh typescript python golang
```

### Option 3: Manual Copy

```bash
# Copy agents
cp agents/*.md ~/.claude/agents/

# Copy rules (common + your language)
cp -r rules/common/* ~/.claude/rules/
cp -r rules/typescript/* ~/.claude/rules/   # pick your stack

# Copy commands
cp commands/*.md ~/.claude/commands/

# Copy skills
cp -r skills/* ~/.claude/skills/
```

### Configure Hooks

Copy hooks from `hooks/hooks.json` to your `~/.claude/settings.json`.

### Configure MCPs

Copy desired MCP servers from `mcp-configs/mcp-servers.json` to your `~/.claude.json`. Replace `YOUR_*_HERE` placeholders with actual API keys.

---

## Running Tests

```bash
# Run all tests (validation + unit tests)
npm test

# Run individual test files
node tests/run-all.js
node tests/lib/utils.test.js
node tests/lib/package-manager.test.js
node tests/hooks/hooks.test.js
```

---

## Cross-Platform Support

All hooks and scripts are written in Node.js for Windows, macOS, and Linux compatibility.

### Package Manager Detection

Automatically detects your preferred package manager with this priority:

1. Environment variable: `CLAUDE_PACKAGE_MANAGER`
2. Project config: `.claude/package-manager.json`
3. `package.json` `packageManager` field
4. Lock file detection (package-lock.json, yarn.lock, pnpm-lock.yaml, bun.lockb)
5. Global config: `~/.claude/package-manager.json`
6. Fallback: first available

```bash
# Set via environment
export CLAUDE_PACKAGE_MANAGER=pnpm

# Set via script
node scripts/setup-package-manager.js --global pnpm
node scripts/setup-package-manager.js --project bun
node scripts/setup-package-manager.js --detect
```

---

## Token Optimization

### Recommended Settings

Add to `~/.claude/settings.json`:

```json
{
  "model": "sonnet",
  "env": {
    "MAX_THINKING_TOKENS": "10000",
    "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "50"
  }
}
```

| Setting | Default | Recommended | Impact |
|---------|---------|-------------|--------|
| `model` | opus | **sonnet** | ~60% cost reduction |
| `MAX_THINKING_TOKENS` | 31,999 | **10,000** | ~70% reduction in thinking cost |
| `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` | 95 | **50** | Compacts earlier for better long-session quality |

### Tips

- Use `/model sonnet` for most tasks, `/model opus` for deep reasoning
- Use `/clear` between unrelated tasks
- Use `/compact` at logical breakpoints
- Use `/cost` to monitor spending
- Keep under 10 MCPs enabled and under 80 tools active

---

## Translations

Full translations available in `docs/`:

| Language | Directory |
|----------|-----------|
| Japanese | `docs/ja-JP/` |
| Simplified Chinese | `docs/zh-CN/` |
| Traditional Chinese | `docs/zh-TW/` |

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Ideas for contributions:**
- Language-specific skills (Rust, C#, Kotlin)
- Framework configs (Rails, Laravel, FastAPI, NestJS)
- DevOps agents (Kubernetes, Terraform, AWS)
- Testing strategies and domain-specific knowledge

---

## License

MIT -- see [LICENSE](LICENSE).

---

**Built by [@drixxodev](https://x.com/drixxodev)**
