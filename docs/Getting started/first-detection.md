---
title: Run Your First Detection
description: How to run file detection with DataSanitizer using Start-DSFileDetection.
sidebar_label: First Detection
sidebar_position: 5
keywords: [DataSanitizer, detection, Start-DSFileDetection, log files, zip, input folder]
---

# Run Your First Detection

To start a detection, use the `Start-DSFileDetection` command. The input folder can contain ZIP files (which will be automatically extracted) or individual files to be analyzed.

## Example Command

```powershell
Start-DSFileDetection -InputPath "C:\DataSanitizer\Org\LogFolder\Input"
```

- **InputPath**: Path to the folder containing files or ZIP archives to process. If not specified, the default configured input folder is used.
- ZIP files are automatically unarchived before detection.
- Results and inventory are saved in the working and inventory folders.

That's it! Your files will be scanned and detection results generated automatically.
