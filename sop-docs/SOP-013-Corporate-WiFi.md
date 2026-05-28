# SOP-013: Corporate WiFi Access

**Category:** network
**Owner:** BSI Network Operations
**Last reviewed:** 2026-01-20

## Purpose
Procedure for connecting BSI-managed devices to corporate WiFi networks and resolving connection issues at Mitsubishi Indonesia offices.

## Scope
All BSI offices in Indonesia: Jakarta (Pulomas HQ + branches), Cikarang plant, Bekasi, and Surabaya. Each site has the same SSID structure.

## Network SSIDs

| SSID | Purpose | Authentication |
|------|---------|----------------|
| `BSI-Corp` | BSI-managed laptops and phones | WPA2 Enterprise, certificate-based (auto via Intune) |
| `BSI-Guest` | Visitor devices, BYOD | Captive portal, sponsored access |
| `BSI-IoT` | Printers, cameras, sensors | Pre-shared key, isolated network |

**Never connect a personal device to `BSI-Corp`.** It will fail authentication and trigger a security alert.

## First-Time Connection (BSI-managed device)

The corporate certificate is pushed via Intune at device enrollment. New laptops should connect automatically when in range.

If the laptop does not auto-connect:
1. Open Windows Settings → Network & Internet → WiFi → Manage known networks
2. Forget `BSI-Corp` if it exists
3. Click `BSI-Corp` from the available networks list
4. Authentication should proceed silently via the device certificate
5. If prompted for username/password, the certificate is missing — see Step 2 below

### Step 2 — Reinstall the WiFi certificate
1. Open Intune Company Portal app
2. Settings → Sync
3. Wait 5 minutes for certificate to push
4. Re-attempt connection

## Common Issues

### Issue: "Cannot connect to this network"
1. Verify WiFi adapter is enabled (Fn+F8 or similar on most ThinkPads)
2. Check if airplane mode is on
3. Try moving closer to the access point (signal weakens through walls)
4. Forget the network and reconnect

### Issue: Connected but no internet
1. Check IP assignment: should be in `10.32.x.x` range
2. If you got `169.254.x.x` (APIPA), DHCP failed — disconnect and reconnect
3. Try `ipconfig /release && ipconfig /renew` in Command Prompt
4. If still no DHCP, escalate — may be a switch port issue

### Issue: WiFi drops repeatedly
1. Check the WiFi adapter driver version (Device Manager → Network adapters)
2. Update to the latest Intel Wireless driver
3. Disable Power Saving on the adapter:
   - Device Manager → adapter → Properties → Power Management → uncheck "Allow the computer to turn off this device"
4. If issue persists in a specific area, report the location — could be an access point problem

### Issue: VPN fails on corporate WiFi
This is normal — `BSI-Corp` already places you on the corporate network. VPN is not needed (and may fail).

Tell the user: "On BSI WiFi, you don't need VPN. Disconnect FortiClient."

## Guest WiFi for Visitors

Visitors should use `BSI-Guest`:
1. Connect to the SSID
2. Browser auto-redirects to the captive portal
3. Visitor enters their email + their BSI sponsor's email
4. Sponsor receives an approval email; click Approve
5. Visitor's device gets internet access for 24 hours

Sponsorship is logged. Heavy users may be asked to use a longer-term solution.

## BYOD (Bring Your Own Device)

Personal devices should NOT use `BSI-Corp`. For personal mobile devices that need access to corporate resources (email, Teams):
1. Enroll the device in Intune (SOP-014)
2. Use `BSI-Guest` for general internet
3. Corporate apps tunnel via the Outlook / Teams mobile apps directly to M365 (no special WiFi needed)

## Escalation
- Single user, persistent issue → L1 + driver reinstall
- Entire floor offline → L2, likely an access point or switch issue
- Captive portal not loading → L2, check the portal server

## Related SOPs
- SOP-001: VPN Access (alternative for off-network)
- SOP-014: Mobile Device Enrollment
- SOP-007: Network Printer Setup
