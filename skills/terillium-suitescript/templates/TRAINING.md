# Training / User Guide Template

> Structure adapted from `MP2 User Guide v1.09.docx` (Office original retained).  
> Embedded screenshots/images were **not** converted. Fill placeholders per feature.

**Product / Feature:** `{{FEATURE_NAME}}`  
**Audience:** `{{AUDIENCE}}`  
**Version:** `{{DOC_VERSION}}`  
**Date:** `{{DOC_DATE}}`

---

## 1. Purpose

{{OBJECTIVE}}

## 2. Who this is for

{{AUDIENCE}}

## 3. What changed

{{CHANGE_SUMMARY}}

## 4. How to use

### 4.1 Prerequisites

{{PREREQUISITES}}

### 4.2 Steps

1. {{STEP_1}}
2. {{STEP_2}}
3. {{STEP_3}}

### 4.3 Expected result

{{EXPECTED_RESULT}}

## 5. Field reference

| Label | Field ID | Notes |
|---|---|---|
| Date | `{{DATE_FIELD}}` | {{DATE_FIELD_NOTES}} |
| Status | `{{STATUS_FIELD}}` | {{STATUS_FIELD_NOTES}} |

## 6. Troubleshooting

| Symptom | Check |
|---|---|
| Status did not update | Confirm date rule, script deployment, role permissions |
| Unexpected status | Confirm `{{STATUS_VALUE}}` mapping and event type (create/edit) |
| Script error | Check Execution Log; confirm `@NAmdConfig` path and deployments |

## 7. Related technical docs

- Technical design: `docs/architecture/{{FEATURE_SLUG}}-technical-diagram.md` (also beside scripts under `integrations/{{FEATURE_SLUG}}/`)
- Script: `{{SCRIPT_FILE}}`

---

## Appendix — source conversion note

The full MP2 User Guide Word file is large (~21MB) and image-heavy. Prefer this structured blank for agent fills. Keep the `.docx` for branded client delivery when screenshots are required.
