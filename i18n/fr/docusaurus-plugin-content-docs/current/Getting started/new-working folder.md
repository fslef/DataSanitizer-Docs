---
title: Initialiser un Nouveau Dossier de Travail
description: Comment préparer un nouveau dossier de travail où la configuration DataSanitizer, les règles de détection et les journaux seront stockés pour les projets d'anonymisation de données.
sidebar_label: Initialiser un Nouveau Dossier de Travail
sidebar_position: 2
keywords: [DataSanitizer, PowerShell, Initialize-DsFolder, dossier, configuration, installation, répertoire de travail]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Initialiser un Nouveau Dossier de Travail

Avant de pouvoir commencer à utiliser DataSanitizer pour analyser et nettoyer vos données, vous devez configurer un dossier de travail correctement structuré. La fonction `Initialize-DsFolder` crée tous les répertoires et fichiers de configuration nécessaires pour commencer.

## Aperçu

La fonction `Initialize-DsFolder` configure un environnement de travail DataSanitizer complet avec :

- **Dossier de configuration** (`_Config`) contenant les paramètres et les règles de détection
- **Dossier intermédiaire** (optionnel) pour organiser les dossiers de journaux avec une classification supplémentaire
- **Structure de dossier de journaux** pour stocker les résultats d'analyse
- **Fichiers de configuration de base** avec les règles de détection par défaut

:::warning[Requis : Dossier Vide]
Vous **devez** utiliser un dossier vide lors de l'initialisation d'un nouveau projet DataSanitizer. La fonction échouera si le dossier cible contient des fichiers pour éviter les écrasements accidentels. Aucun fichier ne sera supprimé - l'opération s'arrête simplement.
:::

## Syntaxe

```powershell
# Avec un dossier intermédiaire
Initialize-DsFolder -RootFolder <CheminRépertoireRacine> -IntermediateFolderName <NomDossierIntermédiaire>

# Sans dossier intermédiaire
Initialize-DsFolder -RootFolder <CheminRépertoireRacine>
```

## Exemples

<Tabs groupId="setup-type">
<TabItem value="basic" label="Configuration de Base">

```powershell
# Créer et initialiser un nouveau projet DataSanitizer
$projectPath = "C:\DataSanitizer\MonProjet"
New-Item -Path $projectPath -ItemType Directory -Force
Initialize-DsFolder -RootFolder $projectPath
```

Ceci crée :

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
<TabItem value="intermediate" label="Avec Dossier Intermédiaire">

```powershell
# Configuration avec dossier intermédiaire pour organiser les dossiers de journaux
$projectPath = "C:\DataSanitizer\ProjetComplexe"
New-Item -Path $projectPath -ItemType Directory -Force
Initialize-DsFolder -RootFolder $projectPath -IntermediateFolderName "Staging"
```

Ceci crée :

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

## Ce qui est Créé

- Dossier `_Config/` avec les fichiers de configuration
  - `DataSanitizer.cfg.json` - Fichier de configuration principal
  - `DetectionRules.cfg.json` - Règles de détection de base
- Dossier `<Intermédiaire>/` si spécifié
- `LogFolder/Input/` où vous placez les fichiers .zip à analyser

## Étapes Suivantes

1. Examiner et personnaliser les règles de détection dans `_Config/DetectionRules.cfg.json`
2. Examiner et personnaliser le fichier de configuration dans `_Config/DataSanitizer.cfg.json`
3. Placer vos fichiers journaux dans `LogFolder/Input/`
4. Exécuter les commandes d'analyse DataSanitizer
