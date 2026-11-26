# Provisioning

A Windows provisioning package (`.ppkg`) that applies the GSecurity configuration to a device.

## Contents

| File | Description |
| --- | --- |
| `GSecurity.ppkg` | Provisioning package named GSecurity, version 1.0. Built for Windows 10.0.26100 (Windows 11 24H2), target SKUs `WindowsCommon`. Not encrypted and not signed. |

## Install

Any of these works:

- **Double-click** `GSecurity.ppkg` and choose **Yes, add it** at the prompt.
- **Settings > Accounts > Access work or school > Add or remove a provisioning package**, then **Add a package**.
- From an elevated PowerShell prompt:

```powershell
Install-ProvisioningPackage -PackagePath .\GSecurity.ppkg -QuietInstall
```

During Windows setup (OOBE), insert the package on a USB drive and the setup flow offers to apply it.

## Inspect before installing

The package is a WIM archive. To see the settings it applies, open it in **Windows Configuration Designer** (part of the Windows ADK or the Microsoft Store app), or run:

```powershell
Get-ProvisioningPackage -PackagePath .\GSecurity.ppkg
```

## Remove

```powershell
Get-ProvisioningPackage | Where-Object PackageName -eq 'GSecurity' | Uninstall-ProvisioningPackage
```

Removing a package does not always revert every setting it applied. Test on a virtual machine first.

## Notes

- The package is unsigned, so Windows shows an unknown-publisher prompt.
- Related: `Policies` (Group Policy backup), `INF` (security templates), `Batch` (scripts).
- `Releases/0.0.1/Provisioning.zip` holds the released copy.

## Author

Gorstak
