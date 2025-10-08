---
title: Initialiser un nouveau répertoire de travail
description: How to prepare a new working folder where DataSanitizer config, detection rules, and logs will be stored for data anonymization projects.
sidebar_label: Nouveau répertoire de travail
keywords: [DataSanitizer, PowerShell, Initialize-DsFolder, folder, configuration, setup, working directory]
---

```powershell
# Avec un dossier intermédiaire
Initialize-DsFolder -RootFolder <CheminRépertoireRacine> -IntermediateFolderName <NomDossierIntermédiaire>

# Sans dossier intermédiaire
Initialize-DsFolder -RootFolder <CheminRépertoireRacine>
```

## Exempleser de travail
description: Comment préparer un nouveau dossier de travail où seront stockés la configuration DataSanitizer, les règles de détection et les journaux pour les projets d'anonymisation de données.
sidebar_label: Initialiser un nouveau dossier de travail
sidebar_position: 4
keywords: [DataSanitizer, PowerShell, Initialize-DsFolder, dossier, configuration, configuration, répertoire de travail]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Initialiser un nouveau dossier de travail

Avant de pouvoir commencer à utiliser DataSanitizer pour analyser et assainir vos données, vous devez configurer un dossier de travail correctement structuré. La fonction `Initialize-DsFolder` crée tous les répertoires et fichiers de configuration nécessaires pour démarrer.

## Vue d'ensemble

La fonction `Initialize-DsFolder` configure un environnement de travail DataSanitizer complet avec :

- **Dossier de configuration** (`_Config`) contenant les paramètres et les règles de détection
- **Dossier intermédiaire** (optionnel) pour organiser les dossiers de journaux avec une classification supplémentaire
- **Structure de dossier de journaux** pour stocker les résultats d'analyse
- **Fichiers de configuration de base** avec les règles de détection par défaut

:::warning[Requis : Dossier vide]
Vous **devez** utiliser un dossier vide lors de l'initialisation d'un nouveau projet DataSanitizer. La fonction échouera si le dossier cible contient des fichiers afin d'éviter les écrasements accidentels. Aucun fichier ne sera supprimé - l'opération s'arrête simplement.
:::

## Syntaxe

```powershell
# With an intermediate folder
Initialize-DsFolder -RootFolder <RootDirectoryPath> -IntermediateFolderName <IntermediateFolderName>

# Without an intermediate folder
Initialize-DsFolder -RootFolder <RootDirectoryPath>
```

## Examples

<Tabs groupId="setup-type">
<TabItem value="basic" label="Configuration de base">

```powershell
# Créer et initialiser un nouveau projet DataSanitizer
$projectPath = "C:\DataSanitizer\MonProjet"
New-Item -Path $projectPath -ItemType Directory -Force
Initialize-DsFolder -RootFolder $projectPath
```

Cela crée :

```text
C:\DataSanitizer\
└── MonProjet\
    ├── _Config\
    │   ├── DataSanitizer.cfg.json
    │   └── DetectionRules.cfg.json
    └── LogFolder\
        └── Input\
```

</TabItem>
<TabItem value="intermediate" label="Avec dossier intermédiaire">

```powershell
# Configuration avec dossier intermédiaire pour organiser les dossiers de journaux
$projectPath = "C:\DataSanitizer\ProjetComplexe"
New-Item -Path $projectPath -ItemType Directory -Force
Initialize-DsFolder -RootFolder $projectPath -IntermediateFolderName "Staging"
```

Cela crée :

```text
C:\DataSanitizer\
└── ProjetComplexe\
    ├── _Config\
    │   ├── DataSanitizer.cfg.json
    │   └── DetectionRules.cfg.json
    └── Staging\
        └── LogFolder\
            └── Input\
```

</TabItem>
</Tabs>

## Ce qui est créé

- Dossier `_Config/` avec les fichiers de configuration
  - `DataSanitizer.cfg.json` - Fichier de configuration principal
  - `DetectionRules.cfg.json` - Règles de détection de base
- Dossier `<Intermédiaire>/` si spécifié
- `LogFolder/Input/` où vous placez les fichiers .zip à analyser

## Prochaines étapes

1. Examinez et personnalisez les règles de détection dans `_Config/DetectionRules.cfg.json`
2. Examinez et personnalisez le fichier de configuration dans `_Config/DataSanitizer.cfg.json`
3. Placez vos fichiers journaux dans `LogFolder/Input/`
4. Exécutez les commandes d'analyse DataSanitizer
