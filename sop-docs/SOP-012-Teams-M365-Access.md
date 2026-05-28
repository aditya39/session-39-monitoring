# SOP-012: Microsoft Teams & M365 Access Issues

**Category:** access
**Owner:** BSI Productivity Services
**Last reviewed:** 2026-03-08

## Purpose
Resolve user-reported issues with Microsoft Teams, OneDrive, SharePoint, and general M365 access.

## Scope
Microsoft 365 services. Excludes Outlook (see SOP-006) and Exchange-specific issues.

## Common Issues

### Issue 1: "We couldn't sign you in to Teams"
Usually a token/cache problem.

Resolution:
1. Quit Teams completely (right-click system tray icon → Quit)
2. Clear the Teams cache:
   - File Explorer → `%AppData%\Microsoft\Teams`
   - Delete the entire folder
   - Also clear `%LocalAppData%\Microsoft\Teams\Cache`
3. Restart Teams
4. Sign in fresh

For the new Teams (v2): the cache location is different:
   - `%LocalAppData%\Packages\MSTeams_8wekyb3d8bbwe\LocalCache`

### Issue 2: Cannot join a meeting
Symptoms vary — could be audio, video, or full failure to connect.

Resolution:
1. Verify the meeting link is current (calendar items can become stale after meeting edits)
2. Test from Teams desktop AND from Teams web (`teams.microsoft.com`)
3. If desktop fails but web works → reinstall Teams desktop
4. Audio issues:
   - Settings → Devices → confirm correct mic/speaker selected
   - Test with the "Make a test call" button
5. Video issues:
   - Confirm no other app is using the camera (Zoom, browser)
   - Check Windows privacy settings allow Teams camera access

### Issue 3: External guest cannot join
B2B guest sign-in issues.

Resolution:
1. Verify the guest user exists in Entra → External Identities → Guests
2. If not, the host needs to invite them as a guest first
3. Guest needs to accept the invitation email (often filtered to spam)
4. Guest must use the email they were invited as — not a personal alias

### Issue 4: OneDrive not syncing
"File sync paused" or files showing as cloud-only when user wants them local.

Resolution:
1. Right-click OneDrive system tray icon → Settings → Account → Stop sync
2. Reconfigure: sign in again with corporate account
3. Choose folders to sync (don't sync everything if space is limited)
4. For Files On-Demand: right-click file → "Always keep on this device"

### Issue 5: SharePoint site access denied
User reports they cannot access a SharePoint site or document library.

Resolution:
1. Verify the user is in the site's permission group (Site Settings → Site Permissions)
2. Check whether the site is part of a Microsoft 365 Group (in which case membership is via the Group)
3. Avoid one-off direct permissions — they don't scale; always use AD groups
4. After permission change, user must close all browser windows and reopen

### Issue 6: Cannot share file externally
Sharing link returns "Sharing is disabled by the administrator."

Resolution:
1. Check the SharePoint site's external sharing setting
2. Default for BSI: external sharing OFF for sensitive sites, ON for collaboration sites
3. If user genuinely needs external sharing, escalate to site owner — they request the change
4. NEVER override security boundary without site owner approval

## Bandwidth and Quality
For users complaining about poor Teams call quality:
1. Check internet bandwidth (`fast.com` or `speedtest.net`)
2. Recommended: 1.5 Mbps up/down minimum for video calls
3. On corporate WiFi, switch to wired if available
4. If on VPN, disconnect for Teams (Teams uses Direct Routing)
5. Close other bandwidth-heavy apps (cloud sync, streaming)

## Escalation
- Recurring issue across many users → check Microsoft 365 Service Health dashboard
- Suspected service outage → notify Service Desk lead + post status page
- Permission issue at site owner level (the owner cannot fix it themselves) → L2

## Related SOPs
- SOP-006: Outlook & Email Issues
- SOP-002: MFA Token Reset
- SOP-013: Corporate WiFi (for quality issues)
