---
title: Fichier de Configuration
description: Apprenez à configurer DataSanitizer avec le fichier de configuration JSON, incluant les paramètres de langue et les chemins.
sidebar_label: Fichier de Configuration
sidebar_position: 4
keywords: [configuration, fichier config, JSON, chemins, paramètres langue, configuration DataSanitizer]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Fichier de Configuration

Le fichier de configuration DataSanitizer est un fichier JSON contenant les paramètres essentiels pour le module.

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

Le paramètre `Version` est défini à `1` et est réservé pour les futures mises à jour du format de configuration.

### Paramètres de Langue (Optionnel)

Les langues sont automatiquement définies selon les paramètres régionaux de l'OS si non spécifiées, mais peuvent être forcées si nécessaire.

- **PSFramework.Localization.Language** : Langue de l'interface console
- **PSFramework.Localization.LoggingLanguage** : Langue des fichiers de log

Les langues supportées sont `"en-US"` et `"fr-FR"`

### Paramètres de Chemin (Obligatoire)

- **DataSanitizer.path.DSrootFolder** : Dossier racine pour les opérations DataSanitizer (contient `_Config` et les dossiers intermédiaires)
- **DataSanitizer.path.DSIncidentFolder** : Dossier d'incident spécifique contenant les données à anonymiser (généralement dans un dossier d'organisation intermédiaire)

:::warning
Les deux paramètres de chemin sont obligatoires pour que l'anonymisation des données fonctionne.
:::

## Exemples

### Configuration Minimale

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
<TabItem value="linux-mac" label="Linux/Mac">

```json
{
    "Version": 1,
    "Static": {
        "DataSanitizer.path.DSrootFolder": "/home/utilisateur/DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "/home/utilisateur/DataSanitizer/Incident01"
    }
}
```

</TabItem>
</Tabs>

### Avec Paramètres de Langue

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

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

</TabItem>
<TabItem value="linux-mac" label="Linux/Mac">

```json
{
    "Version": 1,
    "Static": {
        "PSFramework.Localization.Language": "fr-FR",
        "PSFramework.Localization.LoggingLanguage": "fr-FR",
        "DataSanitizer.path.DSrootFolder": "/home/utilisateur/DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "/home/utilisateur/DataSanitizer/Incident01"
    }
}
```

</TabItem>
</Tabs>

## Charger la Configuration

Une fois que votre fichier de configuration est créé et personnalisé, vous devez le charger dans DataSanitizer en utilisant la commande `Import-DSConfig` :

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

```powershell
Import-DSConfig -ConfigFile "C:\DataSanitizer\_Config\DataSanitizer.cfg.json"
```

</TabItem>
<TabItem value="linux-mac" label="Linux/Mac">

```powershell
Import-DSConfig -ConfigFile "/home/utilisateur/DataSanitizer/_Config/DataSanitizer.cfg.json"
```

</TabItem>
</Tabs>

:::tip
Ajustez le chemin pour correspondre à l'emplacement réel de votre répertoire de travail DataSanitizer. La configuration doit être chargée avant d'exécuter toute commande d'analyse DataSanitizer.
:::
