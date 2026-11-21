# Intune Device Management

## What This Is

Device management with Microsoft Intune, practiced in the free Microsoft 365
Developer Tenant. This repo documents enrolling a Windows device, compliance
policies, app deployment, and the PowerShell detection scripts that go with it.

## Tools Used

- Microsoft Intune (in the M365 Developer Tenant)
- Intune admin center (intune.microsoft.com)
- PowerShell (detection scripts)
- Azure Virtual Machines (the device being managed)

## What I'm Building

- **Device enrollment** — enroll a Windows VM as a managed device in Intune
- **Compliance policy** — require BitLocker and a PIN
- **App deployment** — deploy an app (7-Zip or Chrome) to the VM through Intune
- **Detection script** — a PowerShell script that checks whether the app is
  installed

## Status

In progress — building in the M365 Developer Tenant. Each step will be
documented here with screenshots as it's completed.

## Why It Matters

Enterprises manage thousands of devices through Intune. Enrolling a device,
enforcing compliance, and pushing apps remotely are the day-to-day tasks of
endpoint administration.

## Next Steps

- Enroll the Azure VM (WinVM-01) in Intune
- Create the BitLocker + PIN compliance policy
- Deploy the app and write the detection script
