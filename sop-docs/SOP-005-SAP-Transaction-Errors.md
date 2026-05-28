# SOP-005: SAP Common Transaction Errors

**Category:** ERP
**Owner:** BSI SAP Functional Team
**Last reviewed:** 2026-03-12

## Purpose
Quick reference for resolving the most-reported SAP transaction errors. Covers SD (Sales & Distribution), MM (Materials Management), FI (Finance), and CO (Controlling).

## Scope
Production system PRD-S4H. For QAS or DEV issues, log a separate ticket — Basis handles non-prod.

## Sales & Distribution (SD)

### VA01 — "No customer master exists"
The customer code referenced doesn't exist or is blocked.

Resolution:
1. Verify customer code with transaction XD03
2. Check delivery block, billing block, and posting block on the customer master
3. If customer needs unblocking, escalate to credit management team
4. If new customer needed, follow customer onboarding (separate SOP)

### VA01 — "Pricing error: Mandatory condition PR00 missing"
The material has no list price in the price master for the customer's pricing procedure.

Resolution:
1. Transaction VK13 → enter material + sales org + customer
2. Confirm condition record exists for condition type PR00
3. If missing, contact pricing team to add via VK11
4. Do NOT bypass with manual price unless approved by sales manager

## Materials Management (MM)

### ME21N — "Account assignment is mandatory"
Purchase order requires a cost center or WBS element.

Resolution:
1. Click Account Assignment tab in ME21N
2. Select category K (cost center) or P (project)
3. Enter the cost center the requester gave you
4. If user doesn't know the cost center, route to their manager — never invent a code

### MIGO — "Posting period is closed"
Attempting to post inventory movement to a closed accounting period.

Resolution:
1. Confirm with the requester which period the goods receipt actually belongs to
2. If current period, escalate to FI team to open the period (often closed by mistake)
3. If past period, post to current period and document the variance

## Finance (FI)

### FB60 — "Account requires assignment to CO object"
The G/L account requires a cost center or order assignment for posting.

Resolution:
1. Check transaction KS03 to confirm valid cost centers
2. Enter the appropriate cost center in the line item
3. If unsure which cost center applies, escalate to FI accountant

### F-28 — "Difference too large for clearing"
Customer payment doesn't match outstanding invoice within tolerance.

Resolution:
1. Verify the customer paid the correct invoice (not a different one)
2. Tolerance is set per company code in OBA3 — currently ±IDR 10,000
3. If genuine underpayment, post difference to write-off account `4860000`
4. If genuine overpayment, post to customer credit balance account `2160000`

## Controlling (CO)

### KO01 — "Internal order cannot be created"
Number range may be exhausted or order type misconfigured.

Resolution:
1. Verify order type via KOH3
2. Check number range in CONO
3. If exhausted, request extension via FI team (CO team owns this)

## When NOT to follow this SOP
- If error occurred during month-end close → freeze and call FI lead immediately
- If error has a Note number in SAP (e.g., "see Note 2031234") → search SAP Support Portal first
- If multiple users report the same error simultaneously → likely a configuration issue or batch job failure, escalate

## Escalation
- SD/MM/FI/CO functional issues → respective team (24-hour SLA)
- Month-end close issues → FI lead immediately, P2 incident
- Repeated errors across modules → suspect data corruption, P1 incident

## Related SOPs
- SOP-004: SAP Login & SSO Issues
- SOP-009: Software Install Request
