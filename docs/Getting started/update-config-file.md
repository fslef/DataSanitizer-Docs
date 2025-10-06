---
title: Configuration File
description: Learn how to configure DataSanitizer with the JSON configuration file, including language settings and path parameters.
sidebar_label: Configuration File
sidebar_position: 3
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
        "DataSanitizer.path.DSrootFolder": "C:\\DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "C:\\DataSanitizer\\Incident01"
    }
}
```

## Parameters

### Version

The `Version` parameter is set to `1` and is reserved for future configuration format updates.

### Language Settings (Optional)

Languages are automatically set based on OS locale if not specified, but can be enforced if needed.

- **PSFramework.Localization.Language**: Console interface language
- **PSFramework.Localization.LoggingLanguage**: Log file language

Supported languages are `"en-US"` and `"fr-FR"`

### Path Settings (Required)

- **DataSanitizer.path.DSrootFolder**: Root folder for DataSanitizer operations (contains `_Config` and intermediate folders)
- **DataSanitizer.path.DSIncidentFolder**: Specific incident folder containing data to anonymize (usually within an intermediate organization folder)

:::warning
Both path parameters are mandatory for data anonymization to work.
:::

## Examples

### Minimal Configuration

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

```json
{
    "Version": 1,
    "Static": {
        "DataSanitizer.path.DSrootFolder": "C:\\DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "C:\\DataSanitizer\\Incident01"
    }
}
```

</TabItem>
<TabItem value="linux-mac" label="Linux/Mac">

```json
{
    "Version": 1,
    "Static": {
        "DataSanitizer.path.DSrootFolder": "/home/user/DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "/home/user/DataSanitizer/Incident01"
    }
}
```

</TabItem>
</Tabs>

### With Language Settings

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

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
<TabItem value="linux-mac" label="Linux/Mac">

```json
{
    "Version": 1,
    "Static": {
        "PSFramework.Localization.Language": "en-US",
        "PSFramework.Localization.LoggingLanguage": "en-US",
        "DataSanitizer.path.DSrootFolder": "/home/user/DataSanitizer",
        "DataSanitizer.path.DSIncidentFolder": "/home/user/DataSanitizer/Incident01"
    }
}
```

</TabItem>
</Tabs>

## Loading the Configuration

Once your configuration file is created and customized, you must load it into DataSanitizer using the `Import-DSConfig` command:

<Tabs groupId="operating-systems">
<TabItem value="windows" label="Windows" default>

```powershell
Import-DSConfig -ConfigFile "C:\DataSanitizer\_Config\DataSanitizer.cfg.json"
```

</TabItem>
<TabItem value="linux-mac" label="Linux/Mac">

```powershell
Import-DSConfig -ConfigFile "/home/user/DataSanitizer/_Config/DataSanitizer.cfg.json"
```

</TabItem>
</Tabs>

:::tip
Adjust the path to match your actual DataSanitizer working directory location. The configuration must be loaded before running any DataSanitizer analysis commands.
:::
