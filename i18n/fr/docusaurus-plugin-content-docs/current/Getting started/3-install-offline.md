---
title: Installation hors ligne
description: Étapes rapides pour installer DataSanitizer hors ligne en utilisant un package téléchargé et un script PowerShell.
sidebar_label: Installation hors ligne
keywords: [DataSanitizer, PowerShell, hors ligne, manuel, installation]
---

# Installation hors ligne

1. Téléchargez le fichier `.nupkg` depuis les releases GitHub.
2. Transférez-le vers la machine hors ligne.
3. Exécutez ce script PowerShell (mettez à jour la première variable avec le chemin de votre fichier) :

```powershell
# Chemin vers votre fichier .nupkg
$CheminNuPkg = "C:\Path\To\DataSanitizer.0.3.0-feat.nupkg"

# Trouver le dossier des modules utilisateur
$DossierModule = Join-Path (@([Environment]::GetFolderPath('MyDocuments'), (Join-Path $HOME 'Documents')) | Where-Object { $_ -and (Test-Path $_) } | Select-Object -First 1) 'PowerShell\Modules'
New-Item -ItemType Directory -Path $DossierModule -Force | Out-Null

# Renommer .nupkg en .zip et extraire la version
$CheminZip = $CheminNuPkg -replace '\.nupkg$', '.zip'
Rename-Item $CheminNuPkg $CheminZip -Force
$NomBase = (Get-Item $CheminZip).BaseName
$Version = ($NomBase -replace '^DataSanitizer\.', '').Split('-')[0]
$Destination = "$DossierModule\DataSanitizer\$Version"

# Supprimer l'ancienne version, extraire la nouvelle
if (Test-Path $Destination) { Remove-Item $Destination -Recurse -Force }
New-Item -ItemType Directory -Path $Destination -Force | Out-Null
Expand-Archive -Path $CheminZip -DestinationPath $Destination -Force

# Nettoyer les fichiers NuGet
Remove-Item "$Destination\_rels" -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item "$Destination\[Content_Types].xml" -Force -ErrorAction SilentlyContinue
Remove-Item "$Destination\DataSanitizer.nuspec" -Force -ErrorAction SilentlyContinue

Write-Host "DataSanitizer version $Version installée dans $Destination"
```

---
Il suffit de mettre à jour `$CheminNuPkg` avec le chemin de votre fichier. C'est tout !
