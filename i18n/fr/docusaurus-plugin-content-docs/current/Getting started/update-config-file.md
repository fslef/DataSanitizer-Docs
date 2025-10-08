---
title: Configuration File
description: Learn how to configure DataSanitizer with the JSON configuration file, including language settings and path parameters.
sidebar_label: Configuration File
sidebar_position: 4
keywords: [configuration, config file, JSON, paths, language settings, DataSanitizer setup]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


# Fichier de Configuration

Le fichier de configuration DataSanitizer est un fichier JSON contenant les paramètres essentiels du module.

## Emplacement du Fichier

Le fichier de configuration se nomme `DataSanitizer.cfg.json` et se trouve dans le dossier `_Config` de votre répertoire de travail DataSanitizer.

## Structure de Base

```json
{
    "Version": 1,
    "Static": {
        "PSFramework.Localization.Language": "fr-FR",
        "PSFramework.Localization.LoggingLanguage": "fr-FR",
        "DataSanitizer.path.DSrootFolder": "C:\DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "C:\DataSanitizer\Incident01"
    }
}
```


## Paramètres

### Version

Le paramètre `Version` est défini à `1` et est réservé pour de futures évolutions du format de configuration.

### Paramètres de langue (optionnel)

Les langues sont automatiquement définies selon la langue du système d'exploitation si non spécifiées, mais peuvent être forcées si besoin.

- **PSFramework.Localization.Language** : Langue de l'interface console
- **PSFramework.Localization.LoggingLanguage** : Langue des fichiers de log

Les langues supportées sont `"en-US"` et `"fr-FR"`

### Paramètres de chemin (obligatoire)

**DataSanitizer.path.DSrootFolder** : Dossier racine pour les opérations DataSanitizer (contient `_Config` et les dossiers d'organisation), ex : `C:\DataSanitizer`
**DataSanitizer.path.DSLogInputFolder** : Dossier contenant les fichiers journaux à analyser, ex : `C:\DataSanitizer\Org\LogFolder\Input`
**DataSanitizer.path.DSLogWorkingFolder** : Dossier de travail pour les fichiers journaux en cours de traitement, ex : `C:\DataSanitizer\Org\LogFolder\Working`
**DataSanitizer.Path.DSDetectionRulesFile** : Chemin vers le fichier de configuration des règles de détection, ex : `C:\DataSanitizer\_Config\DetectionRules.cfg.json`
**DataSanitizer.Path.DSFileInventory** : Chemin vers le fichier d'inventaire des fichiers, ex : `C:\DataSanitizer\Org\LogFolder\FileInventory.json`

:::warning
Tous les paramètres de chemin sont obligatoires pour garantir l'anonymisation et l'analyse des données.
:::


## Exemples

### Configuration minimale

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

```json
{
    "Version": 1,
    "Static": {
        "DataSanitizer.path.DSrootFolder": "C:\DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "C:\DataSanitizer\Incident01"
    }
}
```

</TabItem>
<TabItem value="windows-full" label="Windows (complet)">

```json
{
    "Version": 1,
    "Static": {
        "PSFramework.Localization.Language": "fr-FR",
        "PSFramework.Localization.LoggingLanguage": "fr-FR",
        "DataSanitizer.path.DSrootFolder": "C:\\DataSanitizer",
        "DataSanitizer.path.DSLogInputFolder": "C:\\DataSanitizer\\Org\\LogFolder\\Input",
        "DataSanitizer.path.DSLogWorkingFolder": "C:\\DataSanitizer\\Org\\LogFolder\\Working",
        "DataSanitizer.Path.DSDetectionRulesFile": "C:\\DataSanitizer\\_Config\\DetectionRules.cfg.json",
        "DataSanitizer.Path.DSFileInventory": "C:\\DataSanitizer\\Org\\LogFolder\\FileInventory.json"
    }
}
```

</TabItem>
</Tabs>


### Avec paramètres de langue

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

```json
{
    "Version": 1,
    "Static": {
        "PSFramework.Localization.Language": "en-US",
        "PSFramework.Localization.LoggingLanguage": "en-US",
        "DataSanitizer.path.DSrootFolder": "C:\DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "C:\DataSanitizer\Incident01"
    }
}
```

</TabItem>
<TabItem value="windows-full" label="Windows (complet)">

```json
{
    "Version": 1,
    "Static": {
        "PSFramework.Localization.Language": "en-US",
        "PSFramework.Localization.LoggingLanguage": "en-US",
        "DataSanitizer.path.DSrootFolder": "C:\\DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "C:\\DataSanitizer\\Incident01"
    }
}
```

</TabItem>
</Tabs>


## Charger la configuration

Une fois votre fichier de configuration créé et personnalisé, vous devez le charger dans DataSanitizer avec la commande `Import-DSConfig` :

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

```powershell
Import-DSConfig -ConfigFile "C:\DataSanitizer\_Config\DataSanitizer.cfg.json"
```

</TabItem>
<TabItem value="windows-full" label="Windows (complet)">

```powershell
Import-DSConfig -ConfigFile "C:\DataSanitizer\_Config\DataSanitizer.cfg.json"
```

</TabItem>
</Tabs>

:::tip
Adaptez le chemin à l'emplacement réel de votre répertoire de travail DataSanitizer. La configuration doit être chargée avant d'exécuter toute commande d'analyse DataSanitizer.
:::
