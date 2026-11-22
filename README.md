# Intune Device Management

## What This Is

Device management with Microsoft Intune, practiced in the Microsoft 365
Business Premium trial tenant (the free M365 Developer Tenant is not
available to individuals, so the trial is the substitute). This repo
documents enrolling a Windows device, compliance policies, app deployment,
and the PowerShell detection scripts that go with it.

## Tools Used

- Microsoft Intune (in the Microsoft 365 Business Premium trial tenant)
- Intune admin center (intune.microsoft.com)
- PowerShell (detection scripts)
- Azure Virtual Machines (the device being managed)

## What I'm Building

- **Device enrollment** — enroll a Windows VM as a managed device in Intune
  Outcome: Blocked — the VM is not Azure AD joined; needs an interactive RDP session.
- **Compliance policy** — require BitLocker and a PIN — Done Nov 21, 2026
  (see [intune-compliance-policy-summary.pdf](intune-compliance-policy-summary.pdf))
  Outcome: policy 'Require BitLocker and PIN' is live, assigned to All devices.
- **App deployment** — deploy an app (7-Zip or Chrome) to the VM through Intune
  Outcome: Blocked — needs a locally prepared .intunewin package.
- **Detection script** — a PowerShell script that checks whether the app is installed
  Outcome: script written (Test-AppInstalled.ps1 in powershell-toolkit); not yet used in an Intune deployment.

## Status

In progress — the compliance policy is done; enrollment and app deployment
are blocked (see Next Steps). Each step is documented here with summaries
as it's completed.

## Screenshots

- [intune-compliance-policy-summary.pdf](intune-compliance-policy-summary.pdf) — Compliance policy "Require BitLocker and PIN" (Windows 10/11, BitLocker Require, numeric PIN min 4, 41-day expiration, 5 previous PINs, noncompliance marked immediately; assigned to All devices; verified Nov 21, 2026)

## Why It Matters

Enterprises manage thousands of devices through Intune. Enrolling a device,
enforcing compliance, and pushing apps remotely are the day-to-day tasks of
endpoint administration.

## Next Steps

- Enroll the Azure VM (WinVM-01) in Intune — blocked: the VM is not Azure AD
  joined; needs an interactive RDP session to Azure AD join or enroll only
  in device management
- Deploy the app and write the detection script — blocked: app deployment
  needs a locally prepared .intunewin package
- ~~Create the BitLocker + PIN compliance policy~~ — Done Nov 21, 2026
