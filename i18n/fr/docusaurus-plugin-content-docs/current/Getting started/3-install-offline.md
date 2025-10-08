---
title: Installation hors ligne
description: Étapes rapides pour installer DataSanitizer hors ligne en utilisant un package téléchargé et un script PowerShell.
sidebar_label: Installation hors ligne
keywords: [DataSanitizer, PowerShell, hors ligne, manuel, installation]
---

# Installation hors ligne


## 1. Préparation (sur un ordinateur connecté)

1. Téléchargez le fichier `.nupkg` depuis les releases GitHub.
2. Transférez le fichier `.nupkg` vers la machine hors ligne (clé USB, partage réseau, etc.).

## 2. Installation (sur la machine hors ligne)

1. Créer un dossier C:\DS-Install
2. Copier le fichier  `.nupkg` dans ce dossier
3. renommer le  `.nupkg`  en  `.Zip`
4. Extraire l'archive dans le dossier de module Powershell

## Import du module

Pour importer le module :

```powershell
Import-Module DataSanitizer
```

Pour tester que le module est bien chargé

```powershell
Get-Command -Module DataSanitizer
```
