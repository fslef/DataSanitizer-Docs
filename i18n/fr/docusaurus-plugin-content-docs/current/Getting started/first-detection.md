---
title: Exécuter votre première détection
description: Comment exécuter la détection de fichiers avec DataSanitizer en utilisant Start-DSFileDetection.
sidebar_label: Première détection
sidebar_position: 5
keywords: [DataSanitizer, détection, Start-DSFileDetection, fichiers journaux, zip, dossier d'entrée]
---

# Exécuter votre première détection

Pour démarrer une détection, utilisez la commande `Start-DSFileDetection`. Le dossier d'entrée peut contenir des fichiers ZIP (qui seront automatiquement extraits) ou des fichiers individuels à analyser.

## Exemple de commande

```powershell
Start-DSFileDetection -InputPath "C:\DataSanitizer\Org\LogFolder\Input"
```

- **InputPath** : Chemin vers le dossier contenant les fichiers ou archives ZIP à traiter. Si non spécifié, le dossier d'entrée configuré par défaut est utilisé.
- Les fichiers ZIP sont automatiquement décompressés avant la détection.
- Les résultats et l'inventaire sont enregistrés dans les dossiers de travail et d'inventaire.

C'est tout ! Vos fichiers seront analysés et les résultats de détection générés automatiquement.
