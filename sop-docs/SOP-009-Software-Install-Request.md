# SOP-009: Software Installation Request

**Category:** other
**Owner:** BSI End-User Support
**Last reviewed:** 2026-03-05

## Purpose
Standard workflow for installing approved software on BSI-managed laptops. Covers self-service options, request workflow for licensed software, and handling of unapproved software requests.

## Scope
All software installations on BSI-managed Windows laptops. macOS users follow similar workflow with adjusted catalog. Server software is handled separately by Infrastructure team.

## Software Categories

### Tier 1 — Self-Service (Company Portal)
Standard productivity software available without ticket:
- Microsoft 365 Apps (Word, Excel, PowerPoint, Outlook, Teams, OneDrive)
- 7-Zip
- Adobe Acrobat Reader DC
- Google Chrome, Mozilla Firefox
- VLC Media Player
- Notepad++

Install via: Start menu → Company Portal app → search → Install. No ticket needed.

### Tier 2 — Pre-Approved with Auto-Install (Company Portal)
Available in Company Portal but consume a license seat:
- Microsoft Visio
- Microsoft Project
- Adobe Acrobat Pro (paid version, not Reader)
- Power BI Desktop
- SQL Server Management Studio

Install via Company Portal. Manager will receive an automatic notification.

### Tier 3 — Approval Required (Ticket)
Software with significant license cost or security review:
- SAP GUI (auto-installed for SAP users, ticket otherwise)
- Adobe Creative Cloud (full suite)
- AutoCAD / SolidWorks (engineering only)
- Specialized analytics tools (Tableau, Alteryx)
- Programming IDEs (Visual Studio Pro, JetBrains suite)

Submit `SOFTWARE-INSTALL-REQUEST` in ServiceNow with:
- Software name and version
- Business justification (1-2 sentences)
- Manager approval (auto-routed)
- Expected duration of need (project / ongoing)

SLA: 3 business days after manager approval.

### Tier 4 — Not Approved / Requires Exception
- Personal cloud storage clients (Dropbox, Google Drive personal — use OneDrive instead)
- Communication tools outside Teams (WhatsApp Desktop, Telegram, Discord)
- Browser extensions of unknown origin
- Crypto wallets, mining software
- Game launchers (Steam, Epic)

Exception process: requires director-level approval + security review. 2-week SLA. Most are denied.

## Resolution Steps for a Ticket

### Step 1 — Verify the request is Tier 3
If Tier 1 or 2, redirect user to Company Portal. Do not consume a ticket cycle.

### Step 2 — Verify manager approval
Check ServiceNow for the approval workflow status. If pending, ping the manager once. If still pending after 24h, escalate.

### Step 3 — Verify license availability
Check the License Tracker spreadsheet at `\\bsi-fs-01\IT\Licenses\Tracker.xlsx`. If no seats available, hold the install and request procurement.

### Step 4 — Deploy via Intune
For most Tier 3 software, an Intune package exists:
1. Intune admin center → Apps → search the package
2. Assign to the user's device
3. Trigger sync on the user's laptop: Settings → Accounts → Access work or school → Info → Sync
4. App installs in 5-30 minutes depending on size

For software without an Intune package, schedule a remote session with the user to install manually.

### Step 5 — Confirm install and document
Confirm with the user the software launches. Document in ServiceNow:
- License key used (if applicable)
- Tier classification
- Time to resolution

## Unapproved Software Found on a Laptop
Intune scans report unapproved software weekly. When detected:
1. Notify the user (via Teams) — give 5 business days to remove
2. If still installed after 5 days, force uninstall via Intune
3. Document for the user's manager
4. Repeat offenders → escalate to HR

## Escalation
- License not available, project blocker → procurement team + director
- Software requires admin rights to install → L2 (admin rights are restricted)
- Suspected malware bundled with installer → security team immediately

## Related SOPs
- SOP-008: Hardware Request (for software needed at deployment)
- SOP-006: Outlook & Email Issues
- SOP-010: New Employee Onboarding
