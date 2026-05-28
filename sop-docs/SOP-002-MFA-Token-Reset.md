# SOP-002: MFA Token Reset (Microsoft Authenticator)

**Category:** access
**Owner:** BSI Identity & Access Management
**Last reviewed:** 2026-02-28

## Purpose
Procedure for resetting an employee's Multi-Factor Authentication token when they have lost their phone, replaced their device, or the Microsoft Authenticator app has become desynchronized.

## Scope
Applies to all Mitsubishi Indonesia employees with a corporate Microsoft 365 account. Standard Authenticator app only — hardware tokens (YubiKey) are covered separately under SOP-002A.

## Prerequisites
- Verified identity of the requester (see Identity Verification section)
- Employee has access to corporate email OR can be reached via verified mobile number on file
- Ticket logged in ServiceNow before any reset action

## Identity Verification (mandatory)
Before resetting MFA, confirm the requester's identity using TWO of the following:
1. Manager confirmation via separate channel (email or Teams from manager's verified account)
2. NIK (employee ID number) matches HR records
3. Birthdate matches HR records
4. Knowledge-based questions (last project assignment, direct reports, etc.)

**Never reset MFA based on a single channel of identity proof.** Phishing attempts often start with "I lost my phone, please reset my MFA."

## Resolution Steps

### Step 1 — Open Microsoft Entra admin center
URL: `https://entra.microsoft.com` → Users → search for the employee.

### Step 2 — Revoke existing MFA methods
- Click Authentication methods
- Delete the existing Microsoft Authenticator entry
- Sign out of all sessions: Account → Revoke sessions

### Step 3 — Send re-enrollment link
The employee should receive an email prompting them to re-enroll at next sign-in. If the employee cannot access email, generate a temporary access pass (TAP):
- Authentication methods → + Add method → Temporary Access Pass
- Set: One-time use, 1-hour validity
- Provide TAP to employee through a verified channel (NOT email if email is what they're locked out of)

### Step 4 — Guide re-enrollment
1. Employee opens `https://aka.ms/mfasetup` on a trusted device
2. Signs in with their AD password + TAP (if applicable)
3. Adds Microsoft Authenticator from app store
4. Scans the QR code shown in the browser
5. Tests by signing in to outlook.office.com

### Step 5 — Verify resolution
Ask the employee to sign in to a corporate resource (Outlook, Teams) and confirm MFA prompt appears and works.

## Escalation
- If employee fails identity verification → escalate to HR for in-person verification
- If TAP generation fails → escalate to L3 Identity team
- Suspected account compromise → security@bsi.mitsubishi.co.id immediately

## Related SOPs
- SOP-003: Active Directory Password Reset
- SOP-001: VPN Access (MFA prerequisite)
