# SOP-004: SAP Login & SSO Issues

**Category:** ERP
**Owner:** BSI SAP Basis Team
**Last reviewed:** 2026-03-10

## Purpose
Procedure for diagnosing and resolving SAP S/4HANA login failures, including SSO breakdowns, role assignment issues, and concurrent session conflicts.

## Scope
Production SAP system `PRD-S4H` at `sap-prd.bsi.local:3200`. Quality system `QAS-S4H` and development `DEV-S4H` follow similar steps but escalate differently.

## Prerequisites
- AD account is active and not locked (verify per SOP-003)
- VPN is connected if employee is remote (SOP-001)
- SAP GUI version 7.70 patch 12 or later installed

## Common Login Errors

### Error: "User is currently locked"
SAP lock differs from AD lock. Causes:
- Too many failed login attempts (3 max)
- Manual lock by Basis team (security incident)

Resolution:
1. Verify the lock is not security-driven (check ServiceNow for security ticket)
2. Transaction SU01 → enter username → Lock/Unlock button
3. If account shows "Locked by Administrator," do NOT unlock — escalate to security

### Error: "No authorization for transaction X"
The user is missing a role. Common requests:
- VA01 (sales order create) → role `Z_SALES_CREATE`
- ME21N (purchase order create) → role `Z_PROC_CREATE`
- FB01 (post document) → role `Z_FIN_POSTING`

Resolution:
1. Confirm the transaction is appropriate for the user's job function (check with their manager)
2. Submit role request via ServiceNow form `SAP-ROLE-REQUEST`
3. Wait for SoD (Segregation of Duties) approval before assigning
4. Use SU01 → Roles tab → add the approved role
5. Have user log out and back in (roles don't refresh mid-session)

### Error: "Maximum number of sessions reached"
SAP licensing limits concurrent sessions per user (default 6).

Resolution:
1. Have the user close all SAP GUI windows
2. Wait 60 seconds for sessions to time out server-side
3. If urgent, Basis can kill sessions via transaction SM04
4. If user genuinely needs more, request license increase via SAP-LICENSE-REQUEST

### Error: SSO failure — "Logon failed (RC=2)"
The Kerberos ticket isn't reaching SAP.

Resolution:
1. On the user's laptop, open Command Prompt: `klist purge`
2. Sign out of Windows, sign back in
3. Open SAP GUI — SSO should trigger automatically
4. If still failing, fall back to manual SAP password (separate from AD)

## Critical Production Errors

### Database connection lost
If multiple users report inability to connect simultaneously, the database may be down.

Steps:
1. Check the SAP HANA status dashboard at `https://hana-monitor.bsi.local`
2. If red, declare incident immediately
3. Notify on-call SAP Basis: `+62-21-555-0117`
4. Communicate to users via the SAP outage page

## Escalation
- Role authorization issue → SAP Authorization team (24-hour SLA)
- SSO breakdown affecting multiple users → L3 immediately
- Production database issue → P1 incident, page on-call

## Related SOPs
- SOP-005: SAP Common Transaction Errors
- SOP-003: AD Password Reset
- SOP-001: VPN Access
