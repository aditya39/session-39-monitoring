# SOP-006: Outlook & Exchange Email Issues

**Category:** other
**Owner:** BSI Productivity Services
**Last reviewed:** 2026-02-20

## Purpose
Resolve the most common Microsoft Outlook and Exchange Online issues experienced by Mitsubishi Indonesia employees: send/receive failures, calendar sync, large mailbox issues, and shared mailbox access.

## Scope
Microsoft Outlook desktop (current channel, 365 Apps for Enterprise) and Outlook on the web. Mobile Outlook covered separately in SOP-014.

## Prerequisites
- M365 license assigned (verify in Entra)
- Account is not locked
- Internet connectivity (VPN not required for Outlook 365)

## Common Issues

### Issue 1: Outlook cannot connect
Symptoms: "Trying to connect" status bar, password prompt loops.

Resolution:
1. Quit Outlook completely (check Task Manager — no `outlook.exe` running)
2. Open Credential Manager → remove all entries for `*.outlook.office.com` and `*.office365.com`
3. Restart Outlook — it will prompt to sign in fresh
4. If still failing, run Microsoft Support and Recovery Assistant (SaRA): `https://aka.ms/SaRA`

### Issue 2: Mailbox is full
Exchange Online mailboxes are 100 GB by default. Some legacy users may be at 50 GB.

Resolution:
1. In Outlook → File → Cleanup Tools → Mailbox Cleanup
2. Use AutoArchive to move old items to PST or to the In-Place Archive
3. If user needs more than 100 GB, escalate to L2 for license upgrade (E5 includes Auto-Expanding Archive)
4. Verify whether user is shipping large attachments — recommend OneDrive sharing instead

### Issue 3: Calendar items not syncing
Other people see one calendar; the user sees a different one.

Resolution:
1. Confirm user is looking at the correct calendar (default vs shared)
2. Right-click calendar → Properties → check sync status
3. Restart Outlook
4. If still mismatching, recreate the Outlook profile:
 - Control Panel → Mail → Show Profiles → Add → autodiscover with the user's email
 - Set the new profile as default, remove the old one

### Issue 4: Shared mailbox access
User reports they can't see a shared mailbox they should have access to.

Resolution:
1. In Exchange admin center → Recipients → search the shared mailbox
2. Verify the user is in the "Full Access" or "Send As" permission list
3. If permission was granted within the last 60 minutes, it may not have propagated — wait
4. Force the user to refresh: close Outlook, sign out of the mailbox in OWA, restart Outlook
5. Verify the shared mailbox appears under the user's account folder list

### Issue 5: Cannot send to external recipients
Symptoms: NDR with code 550 5.7.1.

Resolution:
1. Verify the recipient address is correct (typos are #1 cause)
2. Check the transport rules in EAC — is there a rule blocking the domain?
3. If blocked legitimately (e.g., competitor domain), explain to user and document
4. If blocked in error, request rule modification via security team

### Issue 6: Phishing email reporting
User says they received a suspicious email.

Resolution:
1. Have the user click the "Report Phishing" button in Outlook (it submits to Microsoft + BSI security)
2. Do NOT forward the email — it can spread links
3. If the user already clicked the link or entered credentials → IMMEDIATE escalation to security, reset password (SOP-003), reset MFA (SOP-002)

## Escalation
- Recurring issue (same user, 3rd ticket on same topic) → L2
- Mailbox migration needed → Exchange admin team
- Suspected phishing or compromise → security@bsi.mitsubishi.co.id immediately

## Related SOPs
- SOP-003: Password Reset
- SOP-002: MFA Token Reset
- SOP-012: Teams & M365 Access
