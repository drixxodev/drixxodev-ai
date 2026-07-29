# Technical Diagram Template

> Companion to `TECHNICAL-DESIGN.md`. Source: TER Technical Design Document structure.

**Feature:** `{{FEATURE_NAME}}`  
**Script:** `{{SCRIPT_FILE}}`  
**Record:** `{{RECORD_TYPE}}`

## Flow

```mermaid
flowchart TD
  trigger["{{TRIGGER_EVENT}}"]
  script["{{SCRIPT_FILE}}"]
  check["Evaluate {{DATE_FIELD}}"]
  setStatus["Set {{STATUS_FIELD}} to {{STATUS_VALUE}}"]
  skip["Leave status unchanged"]
  logErr["log.error and exit"]
  trigger --> script
  script --> check
  check -->|rule met| setStatus
  check -->|rule not met| skip
  script -.->|exception| logErr
```

## Legend

| Symbol | Meaning |
|---|---|
| Trigger | `{{TRIGGER_EVENT}}` |
| Script | `{{SCRIPT_FILE}}` |
| Date field | `{{DATE_FIELD}}` |
| Status field | `{{STATUS_FIELD}}` → `{{STATUS_VALUE}}` |

## Deployment notes

- Script type: `{{SCRIPT_TYPE}}`
- Deployment / audience: `{{DEPLOYMENT_NOTES}}`
- Assumptions: `{{ASSUMPTIONS}}`
