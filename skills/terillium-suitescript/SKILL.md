---
name: terillium-suitescript
description: "Terillium NetSuite SuiteScript 2.1 conventions — file naming, SDF project structure, script patterns, AMD modules, and development workflow for all client repositories"
metadata:
  origin: git-history-analysis
---

# Terillium SuiteScript Development Guide

Conventions and patterns used across all Terillium NetSuite client repositories. Extracted from git history analysis.

## When to Use

Apply these conventions when working in any Terillium SuiteCloud SDF project — any repo with `src/FileCabinet/SuiteScripts/Terillium/` structure, `config.json` AMD aliases, or `ter_ss2_` prefixed scripts.

---

## Technology Stack

- **Platform**: NetSuite (SuiteCloud Development Framework)
- **Runtime**: SuiteScript 2.1 (ES6, AMD `define()`)
- **Module loader**: AMD via `config.json` path aliases
- **Shared library**: TERutils (`ter_utils.js`)
- **SDF project file**: `project.json` at repo root with `defaultAuthId` and `accountSpecificValues`

## Project Structure

```
src/FileCabinet/SuiteScripts/Terillium/
├── _libraries/              # Shared AMD libraries (TERutils, lodash, moment, jQuery, xlsx, crypto)
├── config.json              # AMD path aliases — all scripts reference via @NAmdConfig
└── integrations/
    └── {feature-name}/      # Self-contained integration folder
        ├── ter_ss2_cs_{feature}.js   # ClientScript
        ├── ter_ss2_sl_{feature}.js   # Suitelet
        ├── ter_ss2_ue_{feature}.js   # UserEventScript
        ├── ter_ss2_mr_{feature}.js   # MapReduceScript
        └── ...
```

Each business feature gets its own folder under `integrations/`. All related script types for that feature live together.

## File Naming Convention

```
ter_ss2_{type}_{feature}.js
```

| Abbreviation | Script Type      |
|--------------|-----------------|
| `cs`         | ClientScript    |
| `ue`         | UserEventScript |
| `sl`         | Suitelet        |
| `mr`         | MapReduceScript |
| `ss`         | ScheduledScript |
| `rl`         | RESTlet         |
| `wa`         | Workflow Action  |

The `ter_ss2_` prefix identifies all files as Terillium SuiteScript 2.x. The feature suffix groups related scripts across types.

## Script Header Template

Every file must include this header:

```javascript
/***********************************************************************************
 * @NApiVersion 2.1
 * @copyright [YEAR] Terillium
 * @author Robert Chambliss <rchambliss@terillium.com>
 * @NScriptType [ScriptType]
 * @NModuleScope SameAccount
 * @NAmdConfig ../../config.json
 *
 * Script Description:
 *  [What this script does — 1-2 sentences]
 *
 * Version    Date                  Author                    Remarks
 * 1.00       [Date],               Robert Chambliss          Initial Version
 *
 * @param{log} log
 * @param{record} record
 ***********************************************************************************/
```

Rules:
- `@NAmdConfig` path is relative from the integration folder (typically `../../config.json`)
- `@NModuleScope SameAccount` on all scripts
- Copyright year matches initial creation year
- Version table is updated with every change — date, author, and remark per row

## AMD Module Patterns

### Arrow function style (preferred for new scripts)

```javascript
define(["N/log", "N/record", "N/search"], (log, record, search) => {
  const beforeSubmit = (scriptContext) => { /* ... */ };
  return { beforeSubmit };
});
```

### Function expression style (also accepted)

```javascript
define(["N/currentRecord", "N/record", "N/search", "N/log", "TERutils"],
  function (currentRecord, record, search, log, TERutils) {
    function pageInit(scriptContext) { /* ... */ }
    return { pageInit, fieldChanged, saveRecord };
  }
);
```

Arrow functions are preferred for newer scripts. Both styles are used across the codebase.

## Code Patterns

### Constants Object for Field IDs

Group related field IDs at the top of each module:

```javascript
const FIELDS = {
  SPECIAL_PROJECT: "custcol_special_project",
  BILLING_RATE: "custcol_pem_billing_rate",
  EMPLOYEE: "employee",
};
```

### Guard Clauses for Event Context

Check event type early, wrap in try/catch:

```javascript
const beforeSubmit = (scriptContext) => {
  try {
    if (!isRelevantEventType(scriptContext)) return;
    const { newRecord } = scriptContext;
    // ... logic
  } catch (error) {
    log.error({ title: "Error in beforeSubmit", details: error.message });
  }
};
```

### TERutils Instantiation

```javascript
const utils = new TERutils({ TERutils: TERutils });
```

### Saved Search References

Reference saved searches by string ID:

```javascript
const SEARCH_ID = "customsearch_ter_time_script";
return search.load({ id: SEARCH_ID });
```

### AMD Config (config.json)

All client repos share the same config structure:

```json
{
  "baseUrl": "SuiteScripts/Terillium/",
  "paths": {
    "TERutils": "_libraries/ter_utils.js",
    "lodash": "_libraries/lodash.js",
    "moment": "_libraries/moment.min",
    "jquery": "_libraries/jquery-3.2.1.min",
    "XLSX_lib": "_libraries/xlsx.js"
  }
}
```

## Co-Change Patterns

Scripts within an integration change together in predictable groups:

- **CS + SL** are tightly coupled — UI logic in ClientScript calls Suitelet for server-side rendering
- **UE scripts** change independently — triggered by record events
- **MR scripts** change independently — batch processing with its own lifecycle

When modifying a CS script, always check if the paired SL script needs updates.

## Commit Conventions

Use conventional commits:

```
fix: update production config, exclude items from PEM deal override
refactor: enhance documentation and logging in time revenue script
docs: add comprehensive README summarizing integrations
```

Standard prefixes: `fix:`, `feat:`, `refactor:`, `docs:`, `chore:`, `perf:`



## Document templates

Markdown blanks (converted from Office originals in `templates/`):

| File | Use |
|---|---|
| `templates/TRAINING.md` | User/training guide |
| `templates/TRAINING-DECK.md` | Slide outline |
| `templates/TECHNICAL-DESIGN.md` | TDD blank |
| `templates/TECHNICAL-DIAGRAM.md` | Mermaid diagram blank |

Also mirrored under `docs/templates/suitescript/`. For end-to-end delivery (plan → ship → filled docs in `docs/` **and** `integrations/{feature}/`), use agent **`suitescript-workflow`**. See `SUITESCRIPT-ECC-WALKTHROUGH.md`.

## Development Workflow

1. **Version table first**: Update the header version/remarks table before any code change
2. **Iterative enhancement**: Scripts evolve through multiple commits (initial → features → refactor → config fixes)
3. **Config awareness**: Production vs sandbox config values may differ; check `project.json` `defaultAuthId` and script parameters
4. **Co-change check**: When touching one script in an integration, review sibling scripts for needed updates
5. **Conventional commits**: Use `fix:`, `feat:`, `refactor:`, etc. prefixes
