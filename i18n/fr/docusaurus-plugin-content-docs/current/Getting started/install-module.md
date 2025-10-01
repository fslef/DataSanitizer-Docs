---
title: Installer le module PowerShell DataSanitizer
description: Comment installer (et mettre à jour) le module DataSanitizer dans votre profil utilisateur (sans droits administrateur) et dans des environnements hors ligne ou isolés.
sidebar_label: Installer le module
sidebar_position: 1
keywords: [DataSanitizer, PowerShell, install, module, offline, preview]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Installer le module

La méthode privilégiée pour installer **DataSanitizer** est dans votre profil utilisateur (sans droits administrateur) en utilisant la **dernière version de préversion (preview)** afin de bénéficier des améliorations de détection les plus récentes.

:::info[Pourquoi utiliser la préversion ?]
Le projet est en développement actif. Les builds de préversion contiennent souvent de nouveaux détecteurs, des améliorations de performance et des correctifs de bogues qui ne sont pas encore dans la version stable. Si vous avez besoin d’une stabilité maximale pour des chaînes CI/CD en production, installez plutôt la dernière version stable (omettez `-AllowPrerelease`).
:::

## Installation rapide (profil utilisateur)

<Tabs groupId="channel">
	<TabItem value="preview" label="Préversion (Recommandé)">

```powershell title="Installer la dernière préversion"
Install-Module DataSanitizer -Scope CurrentUser -AllowPrerelease -Force
```

```powershell title="Mettre à jour vers la nouvelle préversion"
Update-Module DataSanitizer -Scope CurrentUser -AllowPrerelease
```

	</TabItem>
	<TabItem value="stable" label="Stable">

```powershell title="Installer la dernière stable"
Install-Module DataSanitizer -Scope CurrentUser -Force
```

```powershell title="Mettre à jour vers la nouvelle stable"
Update-Module DataSanitizer -Scope CurrentUser
```

	</TabItem>
</Tabs>


## Installation hors ligne

Lorsque la machine cible n’a pas accès à Internet :

1. Sur une machine connectée exécutez (inclut les dépendances) :
	 ```powershell
	 Save-Module -Name DataSanitizer -Path ./offline -AllowPrerelease -Force
	 ```
	 (Ou téléchargez le fichier `DataSanitizer.<version>.nupkg` depuis les releases GitHub puis extrayez‑le.)
2. Transférez le dossier `DataSanitizer` vers la machine hors ligne (clé USB, support approuvé, etc.).
3. Copiez‑le dans le chemin des modules utilisateur :

<Tabs groupId="offline-simple">
	<TabItem value="windows" label="Windows">

```powershell
$dest = Join-Path $env:USERPROFILE 'Documents/PowerShell/Modules'
Copy-Item -Path ./DataSanitizer -Destination $dest -Recurse -Force
```

	</TabItem>
	<TabItem value="unix" label="Linux / macOS">

```powershell
$dest = Join-Path $HOME '.local/share/powershell/Modules'
Copy-Item -Path ./DataSanitizer -Destination $dest -Recurse -Force
```

	</TabItem>
</Tabs>

4. Importer & vérifier :
	 ```powershell
	 Import-Module DataSanitizer -Force
	 Get-Module DataSanitizer -ListAvailable | Select Name, Version, Path
	 ```




## Désinstaller / Nettoyer

```powershell
Remove-Module DataSanitizer -ErrorAction SilentlyContinue
Uninstall-Module DataSanitizer -AllVersions -Force
```

## Référence des emplacements des profils PowerShell

<Tabs groupId="ref-paths">
	<TabItem value="windows" label="Windows">

**Chemin des modules utilisateur**

```powershell
$env:USERPROFILE\Documents\PowerShell\Modules
```

  </TabItem>
	<TabItem value="unix" label="Linux / macOS">

**Chemin des modules utilisateur**

```powershell
$HOME/.local/share/powershell/Modules
```

  </TabItem>
</Tabs>

---
Besoin d’aide ? Ouvrez une discussion ou une issue — vos retours aident à améliorer cette documentation d’installation.
