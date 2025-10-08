---
title: Installation hors ligne
description: Étapes rapides pour installer DataSanitizer hors ligne en utilisant un package téléchargé et un script PowerShell.
sidebar_label: Installation hors ligne
keywords: [DataSanitizer, PowerShell, hors ligne, manuel, installation]
---

# Installation hors ligne


## 1. Préparation (sur un ordinateur connecté)

1. Téléchargez le fichier `.nupkg` depuis les releases GitHub.
2. Copiez le script PowerShell ci-dessous dans un fichier, par exemple `Install-DataSanitizer.ps1`.
3. Transférez le fichier `.nupkg` **et** le script PowerShell vers la machine hors ligne (clé USB, partage réseau, etc.).

## 2. Installation (sur la machine hors ligne)

1. Exécutez ce script PowerShell (mettez à jour la première variable avec le chemin de votre fichier) :

```powershell
# Path to your .nupkg file
$NuPkgPath = "C:\Path\To\DataSanitizer.0.3.0-feat.nupkg"

# Find user module folder
$DossierModule = Join-Path (@([Environment]::GetFolderPath('MyDocuments'), (Join-Path $HOME 'Documents')) | Where-Object { $_ -and (Test-Path $_) } | Select-Object -First 1) 'PowerShell\Modules'
New-Item -ItemType Directory -Path $DossierModule -Force | Out-Null

# Rename .nupkg to .zip and extract version
$CheminZip = $NuPkgPath -replace '\.nupkg$', '.zip'
Rename-Item $NuPkgPath $CheminZip -Force
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
Mettre à jour le  `$NuPkgPath` avec le chemin de votre fichier.
