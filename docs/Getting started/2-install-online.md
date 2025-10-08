---
title: Install the DataSanitizer PowerShell Module
description: How to install (and update) the DataSanitizer module in your user profile (no admin rights) and in offline or isolated environments.
sidebar_label: Install Module
sidebar_position: 2
keywords: [DataSanitizer, PowerShell, install, module, offline, preview]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Install the Module

The preferred way to install **DataSanitizer** is in your user profile (non‑admin) and using the **latest preview version** to benefit from the newest detection improvements.

:::info[Why use the preview?]
The project is under active development. Preview builds often contain new detectors, performance improvements, and bug fixes that are not yet in the stable channel. If you need maximum stability for production pipelines, you can install the latest stable instead (omit `-AllowPrerelease`).
:::

## Quick Install (User Profile)

<Tabs groupId="channel">
	<TabItem value="preview" label="Preview (Recommended)">

```powershell title="Install latest preview"
Install-Module DataSanitizer -Scope CurrentUser -AllowPrerelease -Force
```

```powershell title="Update to newest preview"
Update-Module DataSanitizer -Scope CurrentUser -AllowPrerelease
```

	</TabItem>
	<TabItem value="stable" label="Stable">

```powershell title="Install latest stable"
Install-Module DataSanitizer -Scope CurrentUser -Force
```

```powershell title="Update to newest stable"
Update-Module DataSanitizer -Scope CurrentUser
```

	</TabItem>
</Tabs>


...existing code...

## Uninstall / Clean Up

```powershell
Remove-Module DataSanitizer -ErrorAction SilentlyContinue
Uninstall-Module DataSanitizer -AllVersions -Force
```

## Reference PowerShell Profile Locations

<Tabs groupId="ref-paths">
  <TabItem value="windows" label="Windows">

**User module path**

```powershell
$env:USERPROFILE\Documents\PowerShell\Modules
```

  </TabItem>
  <TabItem value="unix" label="Linux / macOS">

**User module path**

```powershell
$HOME/.local/share/powershell/Modules
```

  </TabItem>
</Tabs>

---
Need help? Open a discussion or issue—your feedback helps refine installation docs.
