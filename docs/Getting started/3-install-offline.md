---
title: Offline Install
description: Quick steps for installing DataSanitizer offline using a downloaded package and PowerShell script.
sidebar_label: Offline Install
keywords: [DataSanitizer, PowerShell, offline, manual, install]
---

# Offline Installation


## Preparation (on a connected computer)

1. Download the .nupkg file from the GitHub releases.
2. Transfer the .nupkg file to the offline machine (USB drive, network share, etc.).

## Installation (on the offline machine)

1. Create a folder C:\DS-Install
2. Copy the .nupkg file into this folder
3. Rename the .nupkg file to .zip
4. Extract the archive into the PowerShell module folder

## Import du module

Pour importer le module :

```powershell
Import-Module DataSanitizer
```

Pour tester que le module est bien chagré

```powershell
Get-Command -Module DataSanitizer
```

