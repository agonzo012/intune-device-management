# Intune Device Management

## What This Is

Device management with Microsoft Intune, practiced in the tenant that
comes with the Azure free trial, unblocked by a 30-day Microsoft 365
Business Premium trial (free, $0.00, expires Dec 21, 2026, recurring
billing Off). The M365 Developer Tenant (Instant Sandbox) is not
available — Microsoft now limits the free E5 developer sandbox to
Visual Studio Professional/Enterprise subscribers, partner program
members, or Premier/Unified Support customers, and a personal account
does not qualify. This repo documents enrolling a Windows device,
compliance policies, app deployment, and the PowerShell detection
scripts that go with it.

## Tools Used

- Microsoft Intune (in the Business Premium trial tenant)
- Intune admin center (intune.microsoft.com)
- PowerShell (detection scripts)
- Azure Virtual Machines (the device being managed)

## What I'm Building

- **Device enrollment** — enroll a Windows VM as a managed device in Intune (blocked — see below)
- **Compliance policy** — require BitLocker and a PIN (done Nov 21, 2026)
- **App deployment** — deploy an app (7-Zip or Chrome) to the VM through Intune (blocked — see below)
- **Detection script** — a PowerShell script that checks whether the app is
  installed

## Status

Partly done — see the results from Nov 21, 2026 below.

### WinVM-01 run — Nov 21, 2026

WinVM-01 (AlvinLab-RG, East US 2, Windows Server 2022 Datacenter,
Standard_D2als_v6) was started at 5:39 PM EST, reached Running
~5:52 PM, and was stopped again (deallocated) and confirmed "Stopped
(deallocated)" at 6:06 PM EST. Total run ~27 minutes, a few cents of
the $200 Azure credit. Azure credit: $199.81 of $200 remaining,
expiring Dec 21, 2026.

### Compliance policy — done Nov 21, 2026

"Require BitLocker and PIN" created in Intune (policy ID
79854f87-1715-4c57-bbb9-73b7d7e1b2a4) as a Windows 10/11 compliance
policy. Settings: BitLocker Require; password Require, simple
passwords Block, PIN (Numeric), minimum length 4, expiration 41 days,
previous passwords 5. Noncompliance action: "Mark device noncompliant"
immediately. Assigned to "All devices" (no device is enrolled yet, so
it targets the built-in group).

### Enrollment — blocked

Not done. WinVM-01 is not Azure AD joined (verified via
dsregcmd /status: all NO). Non-interactive enrollment via
deviceenroller.exe /c /AutoEnrollMDM through Run Command failed
(0x80070088) and created no enrollment. Enrolling requires an
interactive RDP session with the VM's local admin credentials to Azure
AD join it or use "Enroll only in device management". Intune
Devices > All devices still shows 0 devices.

### Win32 app deployment — blocked

Not done. The Win32 app flow requires uploading a locally prepared
.intunewin package; none was available in the browser-only workflow.
No app object was created.

### Key finding — subscription visibility

The Azure subscription is owned by the personal account (a guest in
the Default Directory) and is NOT visible to the admin account (0
subscriptions in the Azure portal). Jet completed the MFA registration
for the personal account, after which the Azure portal worked as the
personal account and the VM could be started.

## Why It Matters

Enterprises manage thousands of devices through Intune. Enrolling a device,
enforcing compliance, and pushing apps remotely are the day-to-day tasks of
endpoint administration.

## Next Steps

- Enroll WinVM-01 in Intune — needs an interactive RDP session with
  the VM's local admin credentials to Azure AD join it or use
  "Enroll only in device management".
- Deploy the app — prepare a .intunewin package locally, then upload
  it through the Win32 app flow.
- Write the detection script for the deployed app.
