# SOP-001: VPN Access via FortiClient

**Category:** network
**Owner:** BSI Network Operations
**Last reviewed:** 2026-03-15

## Purpose
Standard procedure for resolving VPN connectivity issues with FortiClient SSL VPN at Mitsubishi Indonesia subsidiaries. Use when an employee reports inability to connect to the corporate network from outside the office.

## Scope
Applies to all BSI-managed laptops running FortiClient v7.0 or later. Excludes BYOD devices (route to SOP-014 Mobile Enrollment).

## Prerequisites
- BSI-issued laptop with FortiClient installed
- Valid Active Directory credentials (use SOP-003 if expired)
- MFA token configured (use SOP-002 if not enrolled)
- Internet connectivity confirmed (ping 8.8.8.8 succeeds)

## Resolution Steps

### Step 1 — Verify FortiClient version
Open FortiClient → About. Confirm version is 7.0.6 or later. If older, escalate to L2 to push the update via Intune.

### Step 2 — Check VPN profile configuration
- Profile name: `BSI-Corp-VPN`
- Gateway: `vpn.bsi.mitsubishi.co.id:443`
- Authentication method: SAML SSO with MFA
- If profile missing, import from `\\bsi-fs-01\IT\FortiClient\bsi-corp-vpn.fcgz`

### Step 3 — Resolve common errors
| Error code | Meaning | Action |
|------------|---------|--------|
| -5029 | SSL VPN tunnel not established | Restart FortiClient service; if persists, reboot |
| -7200 | Authentication failed | Reset password via SOP-003; verify MFA via SOP-002 |
| -8001 | License expired or invalid | Escalate to L2 — license server issue |
| -455 | Server unreachable | Check internet; try 4G hotspot; if fails on both, gateway is down (escalate) |

### Step 4 — Test connection
After connection, verify:
- IP address starts with `10.32.` (corporate subnet)
- Can ping `10.32.1.1` (gateway)
- Can resolve `intranet.bsi.local`

### Step 5 — Document the ticket
Record in ServiceNow:
- FortiClient version
- Error code (if any)
- Resolution applied
- Time to resolution

## Escalation
- After 30 minutes of failed resolution → L2 (Network Operations)
- License or gateway errors → L3 immediately
- More than 5 concurrent users reporting same issue → declare incident, notify on-call lead

## Related SOPs
- SOP-002: MFA Token Reset
- SOP-003: Active Directory Password Reset
- SOP-013: Corporate WiFi Access
