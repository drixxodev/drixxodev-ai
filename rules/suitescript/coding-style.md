> This file extends [common/coding-style.md](../common/coding-style.md) with SuiteScript 2.1 specific content.

# SuiteScript Coding Style

## File Header Template

Every SuiteScript file must include this header:

```javascript
/**
 * @NApiVersion 2.1
 * @copyright 2026 Terillium
 * @author Robert Chambliss <rchambliss@terillium.com>
 * @NScriptType [ScriptType]
 * @NModuleScope SameAccount
 * @NAmdConfig ../../config.json
 *
 * Script Description:
 * [Detailed description of what this script does]
 *
 * Version Date            Author             Remarks
 * 1.00    [Date]          Robert Chambliss   Initial Version
 *
 * @param{record} record
 * @param{search} search
 * @param{log} log
 * @param{TERutils} TERutils
 */
```

## Field Access - Null Protection

Always use fallback values when reading fields:

```javascript
// String field
const poNumber = currentRecord.getValue({ fieldId: 'custbody_po_number' }) || '';

// Number field
const quantity = currentRecord.getValue({ fieldId: 'quantity' }) || 0;

// Date field
const shipDate = currentRecord.getValue({ fieldId: 'shipdate' }) || new Date();

// Sublist value
const lineItem = currentRecord.getSublistValue({
    sublistId: 'item',
    fieldId: 'item',
    line: i
}) || '';
```

## Sublist Iteration

Standard pattern for looping through item lines:

```javascript
const lineCount = currentRecord.getLineCount({ sublistId: 'item' });

for (let i = 0; i < lineCount; i++) {
    const item = currentRecord.getSublistValue({
        sublistId: 'item', fieldId: 'item', line: i
    });
    const quantity = currentRecord.getSublistValue({
        sublistId: 'item', fieldId: 'quantity', line: i
    }) || 0;
    const rate = currentRecord.getSublistValue({
        sublistId: 'item', fieldId: 'rate', line: i
    }) || 0;
}
```

## Logging Levels

```javascript
// Development - use DEBUG and AUDIT
log.debug('Function Start', 'Processing order: ' + orderId);
log.audit('Order Created', 'New SO: ' + salesOrderId);

// Production - use ERROR and EMERGENCY only (saves governance and reduces clutter)
log.error('API Failed', `Warehouse sync failed for order ${orderId}: ${e.message}`);
log.emergency('Critical Failure', 'Database connection lost - stopping script');
```

**Production rule**: Set deployment log level to ERROR or EMERGENCY.

## Script Type Selection

| Script Type | Use When | Governance | Timeout |
|-------------|----------|------------|---------|
| User Event | Real-time single record, validation, must complete synchronously | 1,000 units | 300s |
| Scheduled | Single complex operation, simple sequential workflow | 10,000 units | 5 min target |
| Map/Reduce | Processing 100+ records in batch, need auto-yielding | 10,000/stage | 300s map, 900s reduce |
| Suitelet | Custom UI page, dashboard | 1,000 units | 300s |
| RESTlet | External system calling NetSuite, custom API endpoint | 1,000 units | 300s |

## Governance Monitoring

Always check remaining units in loops or before expensive operations:

```javascript
const script = runtime.getCurrentScript();
const remainingUsage = script.getRemainingUsage();

if (remainingUsage < 100) {
    log.audit('Low Governance', `Only ${remainingUsage} units remaining`);
    return;
}
```

### Governance Start/End Template

```javascript
function processOrders() {
    const script = runtime.getCurrentScript();
    const startingUnits = script.getRemainingUsage();
    log.audit('Governance Start', `Starting with ${startingUnits} units`);

    try {
        // Your code here
    } finally {
        const endingUnits = script.getRemainingUsage();
        const consumed = startingUnits - endingUnits;
        log.audit('Governance End', `Used ${consumed} units, ${endingUnits} remaining`);
    }
}
```

## Governance Unit Costs

| Operation | Units |
|-----------|-------|
| Custom record load/create | 2-4 |
| Custom record save | 4 |
| Standard non-transaction load/create (Customer, Item) | 5 |
| Standard non-transaction save | 10 |
| Standard transaction load/create (Sales Order, Invoice) | 10 |
| Standard transaction save/delete | 20 |
| `search.create()` | Free |
| `search.load()` | 5 |
| `ResultSet.each()` | 10 |
| `ResultSet.getRange()` | 10 |
| `search.lookupFields()` | 1 |
| `email.send()` | 20 |
| `http.get()/post()` | 10 |
| `redirect.toRecord()` | Free |
| `render.transaction()` | 10 |
| `task.create().submit()` | 20 |

## Key Optimization Rules

1. **Use `search.lookupFields()` instead of `record.load()`** when you only need field values (1 unit vs 5-10 units)
2. **Cache loaded records** in a Map -- never reload the same record twice
3. **Only request columns you need** in searches
4. **Use Map/Reduce for bulk operations** instead of looping record.load/save in User Events
5. **Use `record.submitFields()`** for simple field updates instead of load + setValue + save

## Performance Targets

- User Event Scripts: < 5 seconds
- Suitelets: < 10 seconds
- Scheduled Scripts: < 5 minutes
- Map stage: < 300 seconds per invocation
- Reduce stage: < 900 seconds per invocation
