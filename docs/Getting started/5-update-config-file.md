---
title: Configuration File
description: Learn how to configure DataSanitizer with the JSON configuration file, including language settings and path parameters.
sidebar_label: Configuration File
keywords: [configuration, config file, JSON, paths, language settings, DataSanitizer setup]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Configuration File

The DataSanitizer configuration file is a JSON file containing essential settings for the module.

## File Location

The configuration file is named `DataSanitizer.cfg.json` and is located in the `_Config` folder of your DataSanitizer working directory.

## Basic Structure

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

## Parameters

### Version

The `Version` parameter is set to `1` and is reserved for future configuration format updates.

### Path Settings (Required)

- **DataSanitizer.path.DSrootFolder**: Root folder for DataSanitizer operations (contains `_Config` and organization folders), e.g. `C:\DataSanitizer`
- **DataSanitizer.path.DSLogInputFolder**: Folder containing input log files to be analyzed, e.g. `C:\DataSanitizer\Org\LogFolder\Input`
- **DataSanitizer.path.DSLogWorkingFolder**: Folder for working log files during processing, e.g. `C:\DataSanitizer\Org\LogFolder\Working`
- **DataSanitizer.Path.DSDetectionRulesFile**: Path to the detection rules configuration file, e.g. `C:\DataSanitizer\_Config\DetectionRules.cfg.json`
- **DataSanitizer.Path.DSFileInventory**: Path to the file inventory JSON, e.g. `C:\DataSanitizer\Org\LogFolder\FileInventory.json`

:::warning
All path parameters are mandatory for proper data anonymization and analysis.
:::

### Language Settings (Optional)

Languages are automatically set based on OS locale if not specified, but can be enforced if needed.

- **PSFramework.Localization.Language**: Console interface language
- **PSFramework.Localization.LoggingLanguage**: Log file language

Supported languages are `"en-US"` and `"fr-FR"`


## Examples

### Minimal Configuration

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

### With Language Settings

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

## Loading the Configuration

Once your configuration file is created and customized, you must load it into DataSanitizer using the `Import-DSConfig` command:

```powershell
Import-DSConfig -ConfigFile "C:\DataSanitizer\_Config\DataSanitizer.cfg.json"
```

:::tip
Adjust the path to match your actual DataSanitizer working directory location. The configuration must be loaded before running any DataSanitizer analysis commands.
:::
