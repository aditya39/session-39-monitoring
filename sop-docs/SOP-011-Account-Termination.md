# SOP-011: Account Termination (Employee Offboarding)

**Category:** access
**Owner:** BSI Identity & Access Management
**Last reviewed:** 2026-02-25

## Purpose
End-to-end procedure for disabling and eventually deleting a departing employee's IT access. Covers both voluntary departures and terminations.

## Scope
All Mitsubishi Indonesia employees and long-term contractors with BSI-managed accounts.

## SLA Targets
- Disable critical access (email, VPN, ERP): within 1 hour of HR notification
- Disable all account access: within 4 hours
- Final deletion: 90 days after last day (or per legal hold requirements)

## Termination Types

### Type A — Voluntary departure (resignation)
Standard 30-day notice. Planned offboarding.

### Type B — Involuntary termination
HR notifies same-day. Account must be disabled IMMEDIATELY, often before the conversation with the employee.

### Type C — End of contract
Contractor's end date is known in advance. Standard workflow.

## Standard Workflow

### Day -5 (or immediately for Type B)
HR submits the offboarding request via Workday. The system triggers:
1. Manager notification
2. IT pre-offboarding checklist generation
3. Asset return notification

### Day 0 (Last day of work)

#### Hour 0 (morning) — Disable critical access
1. Disable AD account (Properties → Account → "Account is disabled")
2. Revoke all M365 sessions (Entra → Users → Revoke sessions)
3. Block sign-in from all locations
4. Disable VPN access (FortiClient gateway will deny)
5. Set out-of-office auto-reply (delegated to manager)

#### Hour 1-4 — Disable all access
6. Remove from all distribution lists and security groups
7. Disable SAP user (transaction SU01 → Lock)
8. Disable ServiceNow account
9. Disable building access (notify facilities)
10. Forward mailbox to manager for 60 days

#### Hour 4-8 — Asset return
11. Asset team collects laptop, monitor, peripherals at exit interview
12. Sign return form
13. Verify asset tag matches CMDB
14. Laptop wiped and re-imaged for the next user

### Day +30 — Mailbox conversion
- Convert mailbox to "shared mailbox" (no license cost)
- Continue forwarding to manager for another 30 days
- After 60 days total, stop forwarding; mailbox remains shared but no auto-actions

### Day +90 — Final cleanup
- Delete AD account (unless legal hold exists)
- Remove from all systems where they remain
- Archive mailbox content to long-term storage
- Delete cached credentials, certificates, MFA tokens

## Type B — Immediate Termination
When HR notifies of immediate termination:

**Race against time.** Disable in this order:
1. M365 sessions (revoke now — they may be reading email at this moment)
2. VPN (prevent remote re-entry)
3. AD account (prevents new sign-ins)
4. Mobile device wipe via Intune
5. Notify security@bsi.mitsubishi.co.id for monitoring

**DO NOT** delete content. The investigation may need their email, files, Teams messages. Disable, don't destroy.

## Files and Data Handover

### OneDrive
- Files automatically transferred to manager for 30 days
- Manager reviews and migrates anything business-critical to Teams / SharePoint
- After 30 days, files deleted unless flagged for retention

### Teams chats
- Personal chats remain for compliance retention period (7 years)
- Channel posts remain (channel survives the user)
- Manager can request specific message export via eDiscovery

### Shared mailboxes
- Verify the departing user is not the SOLE owner of any shared mailbox
- If yes, reassign ownership BEFORE disabling their account
- Common gotcha — leaves shared mailbox orphaned

## Special Cases

### Legal hold
If HR or legal flags the employee for retention (litigation, investigation):
- Skip the Day +90 deletion
- Keep the mailbox indefinitely (litigation hold)
- Document the retention reason in ServiceNow

### Re-hire within 90 days
If the employee returns within 90 days, reactivate rather than create fresh (see SOP-010).

## Escalation
- Suspected data exfiltration → security team immediately, do NOT delete anything
- VIP / executive offboarding → coordinated with HR + Legal
- Account had elevated privileges → audit log review before deletion

## Related SOPs
- SOP-010: New Employee Onboarding (reverse process)
- SOP-003: Password Reset (often confused with termination)
- SOP-008: Hardware Return (part of asset workflow)
