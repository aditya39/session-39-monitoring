# SOP-010: New Employee IT Onboarding

**Category:** other
**Owner:** BSI Identity & Access Management + Asset Management
**Last reviewed:** 2026-02-10

## Purpose
End-to-end IT setup for new employees joining any Mitsubishi Indonesia subsidiary. Covers identity provisioning, hardware preparation, software baseline, and first-day handover.

## Scope
All new full-time employees and long-term contractors (6+ months). Short-term contractors follow a lighter process (separate SOP).

## Pre-Start Date Checklist

### T-14 days: HR Workday flag triggers
HR creates the employee record in Workday. Workday API pushes the new hire to BSI's onboarding pipeline.

### T-10 days: Identity provisioning
Identity team runs:
1. AD account creation (`firstname.lastname@mitsubishi.co.id`)
2. M365 license assignment (Business Premium for most; E5 for executives/IT)
3. Initial security group memberships based on role
4. MFA enrollment invitation queued (sent T-2 days)
5. ServiceNow user creation
6. Workday SSO link

### T-7 days: Hardware preparation
Asset team:
1. Pull a laptop matching the role's standard config (per SOP-008)
2. Image with the gold image (Windows 11 Enterprise, latest baseline)
3. Apply Intune compliance policies
4. Install Tier 1 software automatically
5. Apply asset tag and security cable
6. Stage in the asset locker for Day 1 pickup

### T-3 days: Email and access verification
Identity team verifies:
- Outlook on the web loads with the new account
- Teams loads
- Test sign-in to all assigned applications

If any access fails, fix before the employee arrives.

### T-2 days: MFA enrollment email sent
Employee receives an email with their AD username + temporary password + MFA enrollment URL. They are instructed to enroll BEFORE Day 1 to save time.

## Day 1 Activities

### Morning (09:00–12:00)
1. **Employee arrives at HR.** HR collects ID documents, signs the IT Acceptable Use Policy.
2. **Employee picks up laptop at Asset Counter.** They sign the Asset Custody Form.
3. **First sign-in.** Employee signs in to the laptop with their AD password. MFA prompt should be ready (because of T-2 enrollment).
4. **Software validation.** Verify Office apps work, OneDrive syncs, Teams connects.

### Afternoon (13:00–17:00)
5. **Role-specific software requests.** Manager submits any Tier 3 software requests (SOP-009).
6. **Department badge & access.** Facilities team handles physical access; IT only handles digital.
7. **Buddy introduction.** Manager assigns a buddy. Buddy walks through internal sites (intranet, ServiceNow, HR portal).

## Day 5 Checkpoint
IT support reaches out via Teams: "How's your laptop? Anything not working?" Catches missed software, broken links, access gaps.

## Day 30 Survey
Automated email asking about the IT onboarding experience. Feedback feeds into SOP improvement.

## Special Cases

### Remote employees
Hardware shipped via courier 5 days before start. Employee picks up at home. Same digital workflow but no in-person handover.

### Returning employees (rehire)
Special handling needed — the system may have the old account in "disabled" state. Identity team reactivates and updates rather than creating fresh. Verify the manager is aware.

### Senior executive
White-glove handling. Identity team coordinator personally walks the executive through setup. C-level executives get additional security configuration (always-on VPN, restricted app catalog).

## Escalation
- Account not ready by Day 1 → P1, all hands on identity team
- Hardware not ready → loaner from Asset Counter while permanent device prepared
- Onboarding flow breaks for multiple new hires same day → investigate Workday integration

## Related SOPs
- SOP-008: Laptop & Hardware Request
- SOP-002: MFA Token Reset (enrollment basis)
- SOP-011: Account Termination (reverse process)
