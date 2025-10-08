---
title: Installer le module PowerShell DataSanitizer
description: Comment installer (et mettre à jour) le module DataSanitizer dans votre profil utilisateur (sans droits administrateur) et dans des environnements hors ligne ou isolés.
sidebar_label: Installer le module
keywords: [DataSanitizer, PowerShell, installer, module, hors ligne, preview]
unlisted: true
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Installer le module

La méthode recommandée pour installer **DataSanitizer** est dans votre profil utilisateur (sans droits administrateur) et en utilisant la **dernière version preview** afin de bénéficier des dernières améliorations de détection.

:::info[Pourquoi utiliser la version preview ?]
Le projet est en développement actif. Les versions preview contiennent souvent de nouveaux détecteurs, des améliorations de performance et des corrections de bugs qui ne sont pas encore disponibles dans la version stable. Si vous avez besoin d'une stabilité maximale pour des pipelines de production, vous pouvez installer la dernière version stable (sans `-AllowPrerelease`).
:::

## Installation rapide (Profil utilisateur)

<Tabs groupId="channel">
	<TabItem value="preview" label="Preview (Recommandé)">

```powershell title="Installer la dernière preview"
Install-Module DataSanitizer -Scope CurrentUser -AllowPrerelease -Force
```

```powershell title="Mettre à jour vers la dernière preview"
Update-Module DataSanitizer -Scope CurrentUser -AllowPrerelease
```

	</TabItem>
	<TabItem value="stable" label="Stable">

```powershell title="Installer la dernière stable"
Install-Module DataSanitizer -Scope CurrentUser -Force
```

```powershell title="Mettre à jour vers la dernière stable"
Update-Module DataSanitizer -Scope CurrentUser
```

	</TabItem>
</Tabs>


...existing code...

## Désinstaller / Nettoyer

```powershell
Remove-Module DataSanitizer -ErrorAction SilentlyContinue
Uninstall-Module DataSanitizer -AllVersions -Force
```

## Références des emplacements du profil PowerShell

<Tabs groupId="ref-paths">
  <TabItem value="windows" label="Windows">

**Chemin du module utilisateur**

```powershell
$env:USERPROFILE\Documents\PowerShell\Modules
```

  </TabItem>
  <TabItem value="unix" label="Linux / macOS">

**Chemin du dossier module pour le profil utilisateur**

```powershell
$HOME/.local/share/powershell/Modules
```

  </TabItem>
</Tabs>

---
Besoin d'aide ? Ouvrez une discussion ou un ticket—vos retours aident à améliorer la documentation d'installation.
