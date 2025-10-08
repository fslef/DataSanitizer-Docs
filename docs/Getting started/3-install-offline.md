title: Offline Install (Manual)
description: Quick steps for installing DataSanitizer offline using a downloaded package and PowerShell script.
sidebar_label: Offline Install
sidebar_position: 3
keywords: [DataSanitizer, PowerShell, offline, manual, install]


# Offline Install (Manual)

1. Download the `.nupkg` file from GitHub releases.
2. Transfer it to the offline machine.
3. Run this PowerShell script (update the first variable with your file path):

```powershell
# Path to your .nupkg file
$CheminNuPkg = "C:\Path\To\DataSanitizer.0.3.0-feat.nupkg"

# Find user module folder
$DossierModule = Join-Path (@([Environment]::GetFolderPath('MyDocuments'), (Join-Path $HOME 'Documents')) | Where-Object { $_ -and (Test-Path $_) } | Select-Object -First 1) 'PowerShell\Modules'
New-Item -ItemType Directory -Path $DossierModule -Force | Out-Null

# Rename .nupkg to .zip and extract version
$CheminZip = $CheminNuPkg -replace '\.nupkg$', '.zip'
Rename-Item $CheminNuPkg $CheminZip -Force
$NomBase = (Get-Item $CheminZip).BaseName
$Version = ($NomBase -replace '^DataSanitizer\.', '').Split('-')[0]
$Destination = "$DossierModule\DataSanitizer\$Version"

# Remove old, extract new
if (Test-Path $Destination) { Remove-Item $Destination -Recurse -Force }
New-Item -ItemType Directory -Path $Destination -Force | Out-Null
Expand-Archive -Path $CheminZip -DestinationPath $Destination -Force

# Clean up NuGet files
Remove-Item "$Destination\_rels" -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item "$Destination\[Content_Types].xml" -Force -ErrorAction SilentlyContinue
Remove-Item "$Destination\DataSanitizer.nuspec" -Force -ErrorAction SilentlyContinue

Write-Host "DataSanitizer version $Version installed in $Destination"
```

---
Just update `$CheminNuPkg` with your file path. That's it!
