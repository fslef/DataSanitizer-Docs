---
title: Fichier de configuration
description: Apprenez à configurer DataSanitizer avec le fichier de configuration JSON, y compris les paramètres de langue et les paramètres de chemin.
sidebar_label: Fichier de configuration
sidebar_position: 5
keywords: [configuration, fichier config, JSON, chemins, paramètres de langue, configuration DataSanitizer]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Fichier de configuration

Le fichier de configuration de DataSanitizer est un fichier JSON contenant les paramètres essentiels du module.

## Emplacement du fichier

Le fichier de configuration se nomme `DataSanitizer.cfg.json` et se trouve dans le dossier `_Config` de votre répertoire de travail DataSanitizer.

## Structure de base

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

Le paramètre `Version` est défini à `1` et est réservé pour les futures mises à jour du format de configuration.

### Paramètres de langue (Optionnel)

Les langues sont automatiquement définies en fonction des paramètres régionaux du système d'exploitation si elles ne sont pas spécifiées, mais peuvent être forcées si nécessaire.

- **PSFramework.Localization.Language** : Langue de l'interface console
- **PSFramework.Localization.LoggingLanguage** : Langue des fichiers journaux

Les langues prises en charge sont `"en-US"` et `"fr-FR"`

### Paramètres de chemin (Requis)

**DataSanitizer.path.DSrootFolder** : Dossier racine pour les opérations DataSanitizer (contient `_Config` et les dossiers d'organisation), par ex. `C:\DataSanitizer`
**DataSanitizer.path.DSLogInputFolder** : Dossier contenant les fichiers journaux d'entrée à analyser, par ex. `C:\DataSanitizer\Org\LogFolder\Input`
**DataSanitizer.path.DSLogWorkingFolder** : Dossier pour les fichiers journaux de travail pendant le traitement, par ex. `C:\DataSanitizer\Org\LogFolder\Working`
**DataSanitizer.Path.DSDetectionRulesFile** : Chemin vers le fichier de configuration des règles de détection, par ex. `C:\DataSanitizer\_Config\DetectionRules.cfg.json`
**DataSanitizer.Path.DSFileInventory** : Chemin vers l'inventaire des fichiers JSON, par ex. `C:\DataSanitizer\Org\LogFolder\FileInventory.json`

:::warning
Tous les paramètres de chemin sont obligatoires pour une anonymisation et une analyse de données appropriées.
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

## Chargement de la configuration

Une fois que votre fichier de configuration est créé et personnalisé, vous devez le charger dans DataSanitizer en utilisant la commande `Import-DSConfig` :

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
Ajustez le chemin pour qu'il corresponde à l'emplacement réel de votre répertoire de travail DataSanitizer. La configuration doit être chargée avant d'exécuter toute commande d'analyse DataSanitizer.
:::
