# SOP-003: Active Directory Password Reset

**Category:** access
**Owner:** BSI Identity & Access Management
**Last reviewed:** 2026-03-01

## Purpose
Standard procedure for resetting an employee's Active Directory password when expired, forgotten, or compromised.

## Scope
All Mitsubishi Indonesia employees with AD accounts. Excludes service accounts (see SOP-003A) and contractor accounts on the partner OU (escalate to L2).

## Password Policy
- Minimum 14 characters
- Must contain uppercase, lowercase, number, special character
- Cannot reuse last 12 passwords
- 90-day expiration
- Account locks after 5 failed attempts (auto-unlock after 30 min OR manual unlock per this SOP)

## Self-service First
Before raising a ticket, employees should try the self-service portal:
- URL: `https://passwordreset.bsi.local`
- Requires registered security questions OR MFA
- Works from anywhere with internet (no VPN needed)

If self-service fails, follow the resolution steps below.

## Identity Verification (mandatory)
Same requirements as SOP-002 — verify via two channels minimum. **Phishing for password resets is a common attack vector at BSI.**

## Resolution Steps

### Step 1 — Open Active Directory Users and Computers
Domain controller: `dc01.bsi.local`. Search the employee's username (firstname.lastname format).

### Step 2 — Reset the password
- Right-click the user → Reset Password
- Generate a complex temporary password (use a password generator, never a pattern)
- Tick "User must change password at next logon"
- Untick "Account is locked out" if applicable

### Step 3 — Deliver temporary password
- For local employees: phone call to verified mobile number, never SMS or email
- For remote employees: voice call via Teams to a verified Teams account
- Document the verification method in the ticket

### Step 4 — Verify the change
Ask the employee to:
1. Connect to corporate VPN (SOP-001) if remote
2. Press Ctrl+Alt+Delete → Change a password
3. Enter the temporary password as current, then their new password twice
4. Confirm sign-in works on outlook.office.com

### Step 5 — Force MFA re-prompt
After password change, force MFA re-prompt on all devices to detect any session hijacking:
- Entra admin center → Users → the user → Revoke sessions

### Step 6 — Document
Record in ServiceNow: verification methods used, reset reason (forgotten / expired / compromised), time to resolution.

## Suspected Compromise
If reset is requested due to suspected compromise:
1. Immediately disable the account first
2. Notify security@bsi.mitsubishi.co.id with the user ID
3. Review last 30 days of sign-in logs in Entra
4. Reset MFA (SOP-002) in addition to password
5. Trigger account review with the employee's manager

## Escalation
- Cannot verify identity → escalate to HR
- Account marked "VIP" or "C-level" → escalate to L3 immediately
- Mass password reset request (more than 5 from one team) → check for ongoing phishing campaign

## Related SOPs
- SOP-002: MFA Token Reset
- SOP-001: VPN Access
- SOP-011: Account Termination (if employee left)
