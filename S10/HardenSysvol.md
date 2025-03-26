# Guide d'Installation et d'Utilisation de HardenSysvol

HardenSysvol est un outil open-source développé par la communauté HardenAD. Il est conçu pour analyser les dossiers SYSVOL et les objets de stratégie de groupe (GPO) dans Active Directory, afin de détecter des données sensibles et des vulnérabilités potentielles. :contentReference[oaicite:0]{index=0}

## Prérequis

- **Système d'exploitation** : Windows avec PowerShell 5.1 ou supérieur.
- **Permissions** : Accès en lecture au dossier SYSVOL de votre domaine Active Directory.

## Installation

### Via la PowerShell Gallery

1. **Ouvrez PowerShell avec des privilèges administratifs** :

   - Cliquez sur le menu Démarrer.
   - Tapez `PowerShell`, faites un clic droit sur **Windows PowerShell**, et sélectionnez **Exécuter en tant qu'administrateur**.

2. **Installez le module HardenSysvol** :

   ```powershell
   Install-Module -Name Hardensysvol -Scope CurrentUser
Remarque : Si c'est la première fois que vous installez un module depuis la PowerShell Gallery, il se peut que vous soyez invité à installer le fournisseur NuGet. Acceptez en tapant Y ou A.

## Téléchargement Manuel depuis GitHub

    1. Accédez au dépôt GitHub de HardenSysvol :

https://github.com/dakhama-mehdi/Harden-Sysvol

    2. Téléchargez la dernière version :

Cliquez sur l'onglet Releases.

Téléchargez le fichier ZIP de la dernière version disponible.

    3. Extrayez le contenu :

Décompressez le fichier ZIP dans le répertoire de votre choix.

    4. Importez le module dans PowerShell :

powershell

Import-Module -Path "Chemin\Vers\Le\Dossier\Hardensysvol\Hardensysvol.psd1"

## Utilisation

Après l'installation, vous pouvez utiliser HardenSysvol pour analyser le dossier SYSVOL de votre domaine.

## Exécuter une Analyse de Base

Pour lancer une analyse simple du dossier SYSVOL :

powershell

Invoke-HardenSysvol

Ce script analysera le dossier SYSVOL à la recherche de données sensibles, telles que des mots de passe en clair ou des informations d'identification stockées dans des scripts ou des fichiers de configuration.

## Options Avancées

HardenSysvol offre plusieurs paramètres pour affiner votre analyse :

  - -Path : Spécifie le chemin du dossier à analyser. Par défaut, il analyse le dossier SYSVOL.

powershell
Invoke-HardenSysvol -Path "C:\Path\To\Custom\Folder"

  - -ReportPath : Définit le chemin où le rapport d'analyse sera sauvegardé.

powershell
Invoke-HardenSysvol -ReportPath "C:\Path\To\Report\report.html"
  
  - -MaxFileSize : Définit la taille maximale des fichiers à analyser (en octets).

powershell
Invoke-HardenSysvol -MaxFileSize 1048576  # 1 Mo

  - -Verbose : Affiche des informations détaillées pendant l'exécution du script.

powershell
Invoke-HardenSysvol -Verbose

## Exemple Complet

Pour exécuter une analyse complète avec un rapport détaillé :

Powershell
Invoke-HardenSysvol -ReportPath "C:\Rapports\HardenSysvol_Report.html" -Verbose

Ce script analysera le dossier SYSVOL et générera un rapport HTML détaillé des résultats dans le dossier spécifié.

## Ressources Supplémentaires

Dépôt GitHub : https://github.com/dakhama-mehdi/Harden-Sysvol

PowerShell Gallery : https://www.powershellgallery.com/packages/Hardensysvol

![Harden](https://github.com/user-attachments/assets/ff5bd4d5-36b9-40fd-9288-7f43d7b22ec3)
---

![Harden2](https://github.com/user-attachments/assets/209ed047-cdb1-42ac-a86a-a37df2014113)
---

![Harden3](https://github.com/user-attachments/assets/dab11942-43f6-4aff-849d-b0c475628df9)
---

![Harden4](https://github.com/user-attachments/assets/bfffa53d-5d09-4d09-96a6-6cb7ecd3446c)
---

![Harden5](https://github.com/user-attachments/assets/45180fba-a7de-4e39-aeaf-b8e0450169fe)
---



