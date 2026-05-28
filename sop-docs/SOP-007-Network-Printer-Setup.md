# SOP-007: Network Printer Setup & Troubleshooting

**Category:** network
**Owner:** BSI End-User Support
**Last reviewed:** 2026-01-30

## Purpose
Procedure for installing network printers on BSI laptops and resolving common print issues across Mitsubishi Indonesia offices.

## Scope
All BSI-managed printers across Jakarta (Pulomas HQ), Cikarang plant, Bekasi, and Surabaya office. Personal USB printers are not supported.

## Print Server Information
- Primary print server: `\\printsrv-jkt-01.bsi.local` (Jakarta + remote)
- Secondary: `\\printsrv-bks-01.bsi.local` (Bekasi + Cikarang)
- Driver repository: `\\bsi-fs-01\IT\Drivers\Printers`

## Resolution Steps

### Step 1 — Identify the printer
Ask the user for:
- Printer name or asset tag (usually a sticker like `PRN-JKT-LT3-01`)
- Floor and location (helps verify the right printer)
- Vendor and model (typically Ricoh MP C4504 or HP LaserJet M608)

### Step 2 — Install via print server
On the user's laptop (must be on corporate network or VPN):
1. Windows key → type `\\printsrv-jkt-01.bsi.local`
2. Wait for the printer list to load
3. Double-click the target printer (e.g., `PRN-JKT-LT3-01`)
4. Windows will install the driver automatically (PCL6 by default)
5. Print a test page from any application

### Step 3 — Common errors

| Error | Cause | Fix |
|-------|-------|-----|
| "Cannot connect to print server" | Not on corporate network | Connect to VPN (SOP-001) or corporate WiFi (SOP-013) |
| "Driver not available" | Architecture mismatch (x86 vs x64) | Manually download driver from `\\bsi-fs-01\IT\Drivers\Printers` |
| "Stuck in queue, jobs pending" | Spooler service hung | Run `net stop spooler && net start spooler` as admin |
| "Out of memory" on large prints | Driver default settings | Change spool option to "Print after last page spooled" |
| "Print job appears blank" | Print-to-PDF redirect | Verify the user selected the network printer, not "Print to PDF" |

### Step 4 — Secure print setup (Ricoh)
Many Ricoh printers at BSI require badge-tap to release jobs (Follow-Me Print).

To enable:
1. Open the printer's Printing Preferences
2. Job Type → select "Locked Print"
3. Set a 4-digit User Code (employee chooses)
4. Print → walk to any Ricoh in the building → tap badge → enter code → release job

### Step 5 — Color vs B&W
By default, all jobs print B&W to control cost. To enable color (requires manager approval):
1. Manager submits request via ServiceNow form `COLOR-PRINT-REQUEST`
2. Approved requests get the user added to the `COLOR-PRINT-USERS` AD group
3. Group membership takes effect at next logon

## Cost Tracking
All print jobs are logged to PaperCut server. Reports run monthly to department managers. If user has unusual volume (>500 pages/month), expect a manager inquiry — encourage digital workflows.

## Escalation
- Hardware issue (jam, paper feed, toner low) → facilities, not BSI
- Driver crash on multiple machines → L2 (likely server-side driver issue)
- Network printer offline for entire floor → L2 + facilities (could be network or printer)

## Related SOPs
- SOP-001: VPN Access (required for remote print)
- SOP-013: Corporate WiFi Access
