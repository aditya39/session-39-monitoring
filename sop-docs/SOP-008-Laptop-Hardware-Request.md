# SOP-008: Laptop & Hardware Request Workflow

**Category:** hardware
**Owner:** BSI Asset Management
**Last reviewed:** 2026-02-15

## Purpose
Procedure for handling employee requests for new laptops, replacements, peripherals, and accessories.

## Scope
All BSI-managed hardware. BYOD (Bring Your Own Device) is a separate program — see SOP-014.

## Standard Hardware Catalog
Pre-approved configurations (no special approval needed beyond standard workflow):

| Role | Standard model | Annual refresh |
|------|----------------|----------------|
| Office worker | Lenovo ThinkPad E14 Gen 5, 16 GB RAM, 512 GB SSD | 4 years |
| Engineer / developer | Lenovo ThinkPad P14s, 32 GB RAM, 1 TB SSD | 3 years |
| Designer / analyst | Lenovo ThinkBook 16p, 32 GB RAM, dedicated GPU | 3 years |
| Field worker | Lenovo ThinkPad L13 Yoga, 16 GB RAM, 256 GB SSD | 4 years |

Non-standard requests (Mac, gaming laptops, etc.) require executive sponsor approval.

## Resolution Steps

### Step 1 — Identify the request type
- **New employee laptop** → start at Step 2A
- **Replacement (existing employee)** → start at Step 2B
- **Peripheral only (monitor, dock, headset)** → start at Step 2C

### Step 2A — New employee
1. Verify the new employee record in HR Workday is approved with a start date
2. Confirm the role to pick the right standard model
3. Submit `ASSET-NEW-LAPTOP` in ServiceNow with the employee's:
 - Full name and employee ID
 - Department and reporting manager
 - Start date and office location
4. Asset team will image the laptop and prepare it for the employee's first day

### Step 2B — Replacement
Check eligibility first:
- Laptop is older than the refresh interval (see catalog above) → automatic
- Laptop is damaged → file insurance claim simultaneously
- Laptop is stolen → file police report + insurance + immediately disable account (SOP-011 for offboarding-like steps)
- Performance issue (laptop too slow) → first try Reimage (saves a request); if still slow, replacement approved

Submit `ASSET-REPLACE-LAPTOP` with reason code (REFRESH / DAMAGE / THEFT / PERFORMANCE).

### Step 2C — Peripherals
Standard peripherals (no approval needed):
- Single 27" monitor (Dell P2723D or equivalent)
- USB-C docking station (Lenovo ThinkPad Universal USB-C Dock)
- Headset (Jabra Evolve2 30)
- Wireless mouse and keyboard (Lenovo Essential set)

Non-standard (manager approval needed):
- Second monitor (must justify use case)
- Webcam (most laptops have one — explain why built-in is insufficient)
- High-end ergonomic peripherals

### Step 3 — Delivery and pickup
For Jakarta HQ: pickup at BSI Asset Counter, Pulomas, Ground Floor, 09:00-17:00 weekdays.
For Cikarang / Bekasi / Surabaya: courier delivery, 5-7 business days.

### Step 4 — Asset registration
Before the user takes the device:
1. Asset team confirms serial number in CMDB
2. User signs the Asset Custody Form
3. User receives standard accessories: power adapter, security cable, asset tag

## Lost / Stolen Devices
**Treat as a security incident immediately.**
1. Disable the AD account (SOP-003-like initial step)
2. Initiate remote wipe via Intune
3. File police report (required for insurance)
4. Notify security@bsi.mitsubishi.co.id
5. Provide a loaner device only after police report is filed

## Escalation
- Non-standard request → manager + department director approval
- Stolen device → security team + HR
- Bulk request (more than 5 devices) → ASSET-BULK-REQUEST form, longer lead time

## Related SOPs
- SOP-009: Software Install Request (for software needed at deployment)
- SOP-010: New Employee Onboarding
- SOP-011: Account Termination (for hardware return)
