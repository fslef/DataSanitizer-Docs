---
title: Initialize a New Working Folder
description: How to prepare a new working folder where DataSanitizer config, detection rules, and logs will be stored for data anonymization projects.
sidebar_label: Initialize New Working Folder
keywords: [DataSanitizer, PowerShell, Initialize-DsFolder, folder, configuration, setup, working directory]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Initialize a New Working Folder

Before you can start using DataSanitizer to analyze and sanitize your data, you need to set up a properly structured working folder. The `Initialize-DsFolder` function creates all the necessary directories and configuration files to get you started.

## Overview

The `Initialize-DsFolder` function sets up a complete DataSanitizer working environment with:

- **Configuration folder** (`_Config`) containing settings and detection rules
- **Intermediate folder** (optional) for organizing log folders with additional classification
- **Log folder** structure for storing analysis results
- **Baseline configuration files** with default detection rules

:::warning[Required: Empty Folder]
You **must** use an empty folder when initializing a new DataSanitizer project. The function will fail if the target folder contains any files to prevent accidental overwrites. No files will be deleted - the operation simply stops.
:::

## Syntax

```powershell
# With an intermediate folder
Initialize-DsFolder -RootFolder <RootDirectoryPath> -IntermediateFolderName <IntermediateFolderName>

# Without an intermediate folder
Initialize-DsFolder -RootFolder <RootDirectoryPath>
```

## Examples

<Tabs groupId="setup-type">
<TabItem value="basic" label="Basic Setup">

```powershell
# Create and initialize a new DataSanitizer project
$projectPath = "C:\DataSanitizer\MyProject"
New-Item -Path $projectPath -ItemType Directory -Force
Initialize-DsFolder -RootFolder $projectPath
```

This creates:

```text
C:\DataSanitizer\
└── MyProject\
    ├── _Config\
    │   ├── DataSanitizer.cfg.json
    │   └── DetectionRules.cfg.json
    └── LogFolder\
        └── Input\
```

</TabItem>
<TabItem value="intermediate" label="With Intermediate Folder">

```powershell
# Setup with intermediate folder for organizing log folders
$projectPath = "C:\DataSanitizer\ComplexProject"
New-Item -Path $projectPath -ItemType Directory -Force
Initialize-DsFolder -RootFolder $projectPath -IntermediateFolderName "Staging"
```

This creates:

```text
C:\DataSanitizer\
└── ComplexProject\
    ├── _Config\
    │   ├── DataSanitizer.cfg.json
    │   └── DetectionRules.cfg.json
    └── Staging\
        └── LogFolder\
            └── Input\
```

</TabItem>
</Tabs>

## What Gets Created

- `_Config/` folder with configuration files
  - `DataSanitizer.cfg.json` - Main configuration file
  - `DetectionRules.cfg.json` - Baseline detection rules
- `<Intermediate>/` folder if specified
- `LogFolder/Input/` where you place files of .zip to analyze

## Next Steps

1. Review and customize detection rules in `_Config/DetectionRules.cfg.json`
2. Review and customize configuration file in `_Config/DataSanitizer.cfg.json`
3. Place your log files in `LogFolder/Input/`
4. Run DataSanitizer analysis commands
