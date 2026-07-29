# ECC SuiteScript walkthrough

Copy/paste prompts for Terillium SuiteScript 2.1 work with Everything Claude Code. Work in a **client SDF repo**, not inside this toolbox (`drixxodev-ai`).

**Preferred:** invoke the **`suitescript-workflow`** agent — it runs phases 1–8, applies `terillium-suitescript` + `rules/suitescript`, loops until the objective is met, and fills training + technical diagram templates into **both** client `docs/` and `integrations/{feature}/`.

```
Use the suitescript-workflow agent for: Sales Order User Event that sets a status field based on a date field. Follow terillium-suitescript and rules/suitescript.
```

After adding/editing the agent: copy to `~/.claude/agents/` (or re-run install) and start a **new** session.

---

## Skills, rules, and templates

| Asset | Role |
|---|---|
| Agent `suitescript-workflow` | Full process owner |
| Skill `terillium-suitescript` | Naming, SDF layout, AMD, header, version table |
| Skill `plan-orchestrate` | Optional multi-step → `/orchestrate` lines |
| `rules/suitescript/*` | coding-style, patterns, security, testing |
| `docs/templates/suitescript/` (and `skills/terillium-suitescript/templates/`) | `TRAINING.md`, `TECHNICAL-DIAGRAM.md`, `TECHNICAL-DESIGN.md`, `TRAINING-DECK.md` |

**Name the skill and rules in prompts** — auto-trigger is usual but not guaranteed.

---

## Template locations

**Blanks (toolbox):** `docs/templates/suitescript/` and `skills/terillium-suitescript/templates/` (Office originals kept beside the MD).

**Filled (client repo) — both destinations required:**

1. `docs/training/{feature}-training.md` + `docs/architecture/{feature}-technical-diagram.md`
2. `src/FileCabinet/SuiteScripts/Terillium/integrations/{feature}/` — both guides beside `ter_ss2_*` scripts

---

## Full session (phases)

### 1. Plan

**What:** Restate goal, risks, steps; write OBJECTIVE + ACCEPTANCE; wait for OK.  
**Skills/rules:** `terillium-suitescript` + `rules/suitescript`.

```
/plan Add a SuiteScript 2.1 User Event in a Terillium SDF project. Follow skill terillium-suitescript and rules/suitescript (coding-style, patterns, security, testing). On {{RECORD_TYPE}} beforeSubmit (create/edit), if {{DATE_FIELD}} meets the rule, set {{STATUS_FIELD}} to {{STATUS_VALUE}}. Null-safe field reads, FIELDS constants, Terillium header + version table, AMD define. File ter_ss2_ue_{feature}.js under integrations/{feature}/. No hardcoded secrets. Sandbox-first.
```

```
Looks good — proceed.
```

**Gate:** User must say proceed before Build.

---

### 2. Optional — plan-orchestrate

Run once if the plan has multiple steps; paste **one** `/orchestrate` line per message (Enter, wait).

```
plan-orchestrate @.claude/plan/{feature}.md --lang=auto
```

Same plan file every time; different `#step-N` commands.

---

### 3. Build

**What:** Implement script; version table first.  
**Skills/rules:** terillium-suitescript + coding-style / patterns / security.

```
Implement per the plan. Use skill terillium-suitescript and apply rules/suitescript. Update the version table before code changes. Put the file under src/FileCabinet/SuiteScripts/Terillium/integrations/{feature}/.
```

**Next:** Auto → Review when files are written.

---

### 4. `/code-review`

```
/code-review — check against rules/suitescript (null field access, secrets/script params, governance, header version table) and terillium-suitescript naming/AMD. Verify ACCEPTANCE.
```

CRITICAL/HIGH → fix and re-enter Build → Review (objective loop).

---

### 5. `/build-fix` (only if broken)

```
/build-fix — SuiteCloud / SDF validate failed with: <paste error>
```

Skip if validate is green.

---

### 6. Sandbox verify

```
Walk the SuiteScript pre-deploy checklist from rules/suitescript/testing.md for this script: 1-record happy path, missing/null date, create vs edit, status mapping, affected roles. List what I must verify in sandbox.
```

**Gate:** You report results. Agent must not invent a pass. Fail → loop to Build (or Plan if acceptance was wrong).

---

### 7. Ship gate + docs

```
Security and ship gate against rules/suitescript/security.md and testing.md: no hardcoded credentials; log level; rollback; deploy window. PASS/FAIL. On PASS, fill TRAINING.md and TECHNICAL-DIAGRAM.md into docs/ and integrations/{feature}/.
```

---

### 8. `/learn` + `/save-session`

Only after OBJECTIVE MET. Two messages:

```
/learn
```

```
/save-session
```

---

## Phase gates (when next starts)

| Transition | Starts when |
|---|---|
| Plan → Build | You say **proceed** |
| Build → Review | Code written (**auto**) |
| Review → Sandbox | Review clean (**auto**; else loop) |
| Sandbox → Ship | **You** report sandbox results |
| Ship → Learn | `SHIP: PASS` |
| Errors / unmet objective | **Re-enter** Plan or Build; soft cap 3 retries per failure class |

---

## Minimal path

Invoke `suitescript-workflow` with the date→status goal → approve plan → let it build/review → run sandbox checks → confirm → ship docs → `/learn` + `/save-session`.

---

## What not to do

- Don’t implement client SuiteScript only inside `drixxodev-ai`
- Don’t skip naming `terillium-suitescript` / `rules/suitescript` when it matters
- Don’t paste multiple `/orchestrate` lines in one message
- Don’t mark Done while ACCEPTANCE fails — loop
- Don’t hardcode secrets

---

## Related

- [OWNER-QUICKSTART.md](OWNER-QUICKSTART.md)
- [NEXTJS-ECC-WALKTHROUGH.md](NEXTJS-ECC-WALKTHROUGH.md)
- [skills/terillium-suitescript/SKILL.md](skills/terillium-suitescript/SKILL.md)
- [skills/terillium-suitescript/templates/README.md](skills/terillium-suitescript/templates/README.md)
- [docs/templates/suitescript/README.md](docs/templates/suitescript/README.md)
- [agents/suitescript-workflow.md](agents/suitescript-workflow.md)
