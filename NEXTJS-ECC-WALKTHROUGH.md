# ECC Next.js calculator walkthrough

Copy/paste prompts for building a small Next.js calculator site with Everything Claude Code (ECC). Work in a **separate project folder** (e.g. `~/Projects/calc-site`), not inside this toolbox repo (`drixxodev-ai`).

---

## Full session

### 1. Plan first

```
/plan Build a small Next.js App Router calculator website: basic +, -, ×, ÷, clear, and decimal. Single-page, keyboard-friendly, mobile-usable. No auth, no backend. Ship-ready polish (layout, a11y labels, SEO title/description).
```

Wait for the plan. Reply:

```
Looks good — proceed.
```

---

### 2. Optional — multi-step with plan-orchestrate

Use this when the plan has several steps and you want a controlled agent chain per step. For a tiny calculator you can skip to section 3.

Run **once**:

```
plan-orchestrate @.claude/plan/calc.md --lang=typescript
```

(Use the real plan file path `/plan` wrote.)

It prints **one `/orchestrate` line per step**. Paste them **one chat message at a time**.

**Not** re-running `plan-orchestrate` with a different filename each time.  
**Not** several `/orchestrate` commands on one line.

| Message # | What you paste | Then |
|---|---|---|
| 1 | `plan-orchestrate @.claude/plan/calc.md --lang=typescript` | Send once. Read the printed commands. |
| 2 | Only the Step 1 `/ecc:orchestrate custom "…" "…"` line | Send. Wait until finished. |
| 3 | Only the Step 2 line | Send. Wait. |
| 4 | Only the Step 3 line | Send. Wait. |

Same plan file (`calc.md`) every time. What changes is `#step-1` / `#step-2` / …  
Rule: **one chat message = one command = press Enter once = wait.**

Example lines you might get back:

```bash
/ecc:orchestrate custom "ecc:tdd-guide,ecc:typescript-reviewer" "[Plan: .claude/plan/calc.md#step-1] Implement pure calculator engine (+ - * / clear decimal) with unit tests; Acceptance: divide-by-zero returns Error; chained ops behave like a basic calculator"

/ecc:orchestrate custom "ecc:tdd-guide,ecc:typescript-reviewer" "[Plan: .claude/plan/calc.md#step-2] Build client Calculator keypad + display wired to the engine; Acceptance: click and keyboard paths both work; large mobile tap targets"

/ecc:orchestrate custom "ecc:doc-updater,ecc:typescript-reviewer" "[Plan: .claude/plan/calc.md#step-3] Add title/meta description and a11y labels; Acceptance: one H1; meta description present; buttons have accessible names"
```

(Legacy install uses `/orchestrate` and bare agent names instead of `/ecc:orchestrate` + `ecc:` prefixes.)

Scope tricks:

```
plan-orchestrate @.claude/plan/calc.md --lang=typescript --scope=step:2
plan-orchestrate @.claude/plan/calc.md --lang=typescript --scope=range:1-2
plan-orchestrate @.claude/plan/calc.md --lang=typescript --dry-run
```

---

### 3. Plain-English build (or skip §2)

```
Scaffold a Next.js App Router + TypeScript + Tailwind app if one doesn't exist yet. Then build a single-page calculator: display, number pad, operators, clear, decimal. Use server components where possible; client component only for the interactive keypad. Make it keyboard-accessible (Enter/=, Escape to clear, number keys). Keep the first viewport simple — one calculator composition, no dashboard layout.
```

Follow-ups as needed:

```
Add unit tests for the pure calc logic (not the UI). Cover divide-by-zero and chained operations.
```

```
Polish mobile layout at 375px — large tap targets, no overflow.
```

```
Add page title and meta description for SEO. No blog, no extra pages.
```

---

### 4. `/code-review` — quality + security pass

**What it is:** A structured review of your uncommitted (or recent) changes — readability, bugs, security, maintainability. Not a rewrite; it flags issues by severity.

**When:** After the calculator code exists and you’re happy enough to ship-or-fix. Do this **before** treating the feature as done.

**What to type:**

```
/code-review
```

**What “done” looks like:** You get CRITICAL / HIGH / MEDIUM / LOW findings. Fix CRITICAL and HIGH (or consciously accept). Re-run `/code-review` if you changed a lot.

**Calculator tip:** Watch for unsafe `eval`, missing divide-by-zero handling, and a11y gaps on buttons.

---

### 5. `/build-fix` — only when the build is broken

**What it is:** Minimal, surgical fixes when `next build` / `tsc` / the bundler fails. For Next.js, this often routes to a React/Next build resolver (hydration, server/client boundaries, config).

**When:** Only if the app won’t compile or run. Skip this step if everything builds clean.

**What to type:**

```
/build-fix
```

Or, if you already know the error:

```
/build-fix — next build fails with: <paste error>
```

**What “done” looks like:** `next build` (or `npm run build`) succeeds again. Don’t use this for feature work — only for green builds.

---

### 6. `/e2e` — prove the money path in a browser

**What it is:** Generates and/or runs end-to-end tests (usually Playwright) against the running app — click through like a user.

**When:** After the UI works manually. For a calculator, one happy path + clear is enough.

**What to type:**

```
/e2e Cover: load page, type 12 + 3 = and assert 15; clear resets display.
```

**Prereq:** Dev server up (e.g. `http://localhost:3000`) unless the command starts it for you.

**What “done” looks like:** Tests pass (or you get a clear failure + screenshot/trace). Fix failures before the ship gate.

---

### 7. `release-gatekeeper` — ship / don’t-ship

**What it is:** One PASS/FAIL gate that runs the QA pack against a URL:

- `site-health-sentinel` — pages load, no obvious broken links/console wreckage
- `lead-flow-tester` — lead forms work (often N/A for a pure calculator; still fine to run)
- `seo-content-auditor` — title, meta, headings publish-ready
- `responsive-visual-qa` — layout at mobile / tablet / desktop widths

**When:** Right before you deploy or share a preview. Don’t skip for client work; for a personal toy calc it’s still good practice once.

**What to type:**

```
Run release-gatekeeper against http://localhost:3000. I need a PASS/FAIL before I deploy.
```

Use your preview/prod URL instead of localhost when that’s what you’re shipping.

**Piecemeal (if you only want parts):**

```
Run responsive-visual-qa on the calculator page at 375, 768, and 1280.
```

```
Run seo-content-auditor on the home page.
```

**What “done” looks like:** A clear **PASS** or **FAIL** with why. Fix FAILs, re-run, then deploy.

---

### 8. `/learn` + `/save-session` — bank knowledge, carry context

**What `/learn` is:** Pulls reusable patterns from this session into a skill/instinct so you don’t re-solve the same calculator/Next.js quirks next time.

**What `/save-session` is:** Snapshots session state so tomorrow’s `/resume-session` can continue without re-explaining the project.

**When:** End of a good session (or end of day). `/learn` after something worked well; `/save-session` whenever you’ll come back later.

**What to type (two separate messages):**

```
/learn
```

```
/save-session
```

**What “done” looks like:** Learn confirms something was captured (or says nothing new). Save confirms a session snapshot exists. Next day start with `/resume-session` if you want that context back.

---

## Minimal path

If you want the shortest useful loop for a toy calculator:

```
/plan Small Next.js calculator site: + - × ÷ clear decimal, single page, a11y + mobile, no backend.
```

(approve)

```
Build it now per the plan. App Router, TypeScript, Tailwind. Pure logic tested. Client keypad only.
```

```
/code-review
```

```
Run release-gatekeeper on http://localhost:3000
```

---

## What not to type

- Don’t build the calculator **inside** `drixxodev-ai` — open a separate site repo
- Don’t invent flags like `/orchestrate --mode=...` — use `custom "agents" "task"` only
- Don’t paste multiple `/orchestrate` lines in one message
- Don’t re-run `plan-orchestrate` with a different filename for each step — same plan file; paste a different step command each message
- Don’t send Step 2 before Step 1’s agent chain has finished
- Don’t skip approval after `/plan` if you want the safe ECC habit

---

## Related

- [OWNER-QUICKSTART.md](OWNER-QUICKSTART.md) — day-to-day ECC loop
- [COMMANDS-QUICK-REF.md](COMMANDS-QUICK-REF.md) — full command list
- [skills/plan-orchestrate/SKILL.md](skills/plan-orchestrate/SKILL.md) — plan → orchestrate bridge
- [SUITESCRIPT-ECC-WALKTHROUGH.md](SUITESCRIPT-ECC-WALKTHROUGH.md) — SuiteScript / Terillium ECC process
