# PingCastle

# Guide d'utilisation et d'analyse de PingCastle

## Sommaire
1. [Installation de PingCastle](#installation-de-pingcastle)
2. [Exécution d'un audit de sécurité](#exécution-dun-audit-de-sécurité)
3. [Types d'analyses et options](#types-danalyses-et-options)
4. [Interprétation des résultats](#interprétation-des-résultats)
5. [Actions correctives](#actions-correctives)
6. [Bonnes pratiques](#bonnes-pratiques)

---

## Installation de PingCastle
---

### Prérequis
  -  Windows Server ou Windows client (7+)
  - .NET Framework 4.5+
  - Compte avec droits de lecture sur l'Active Directory

### Étapes d'installation
1. Télécharger la dernière version de PingCastle depuis [le site officiel](https://www.pingcastle.com/download)
2. Extraire l'archive ZIP dans un répertoire dédié
3. Aucune installation n'est nécessaire - PingCastle fonctionne en mode portable

### Vérification de l'installation

##### Naviguer vers le répertoire d'extraction

  - cd C:\chemin\vers\PingCastle

##### Vérifier que PingCastle fonctionne correctement
  
  - .\PingCastle.exe --help

### Exécution d'un audit de sécurité

#### Analyse healthcheck standard

##### Exécuter un healthcheck complet
  
  - .\PingCastle.exe --healthcheck

##### Avec authentification spécifique

  - .\PingCastle.exe --healthcheck --server dc01.domaine.local --user utilisateur --password motdepasse
---

## Analyse programmée

##### Créer une tâche planifiée pour des audits réguliers

  - .\PingCastle.exe --generate-scheduled-task --task-name "PingCastle-Monthly" --healthcheck --report-dir "C:\Rapports\PingCastle" --periodicity monthly

#### Création d'un rapport de base

    1.Lancer l'analyse via l'interface de commande
    
    2.Attendre la fin de l'analyse (durée variable selon la taille de l'AD)
    
    3.Accéder au rapport généré (format HTML) dans le répertoire courant ou spécifié

### Types d'analyses et options

#### Options d'analyse principales

##### Exemples d'autres analyses

###### Commande
    
    - --explorer :	Explorer la structure de l'AD

    - --localadmin: Scanner les droits admin locaux

    - --graph	Analyser : les relations entre objets AD

    - --nullsession :	Vérifier les vulnérabilités des sessions nulles

    - --aclcheck : Analyse des permissions ACL

#### Exemples courants

##### Exécuter un healthcheck pour un domaine spécifique

  - .\PingCastle.exe --healthcheck --domain autredomaine.local

##### Exporter un rapport détaillé

  - .\PingCastle.exe --healthcheck --report-dir "C:\Rapports\AD"

##### Générer une cartographie des relations de confiance AD

  - .\PingCastle.exe --carto

#### Regrouper plusieurs rapports

Si vous avez plusieurs rapports PingCastle, vous pouvez les consolider :

  - .\PingCastle.exe --conso --input-dir "C:\Rapports\Multiple"

### Actions correctives

#### Suivi des privilèges élevés

##### Identifier les comptes sensibles

  - Get-ADGroupMember "Admins du domaine" | Select-Object Name, SamAccountName

##### Vérifier les comptes appartenant aux groupes sensibles

  - Get-ADUser -Filter * -Properties MemberOf | Where-Object {$_.MemberOf -match "CN=Admins du domaine"} | Select-Object Name

##### Renforcement de l'infrastructure

    1. Appliquer les mises à jour disponibles sur les contrôleurs de domaine (Domain Controllers).

    2. Désactiver les protocoles obsolètes tels que SMBv1 ou NTLMv1.

    3. Activer LDAP signing et SMB signing pour sécuriser les communications.

### Suivi et bonnes pratiques

#### Stratégies d'audit

    1. Planifiez des audits mensuels pour maintenir une vue continue de la sécurité de l'Active Directory.

    2.Exécutez des analyses immédiatement après des modifications d'infrastructure significatives.

#### Documentation

    1. Stockez les rapports générés de manière organisée dans des dossiers à date unique.

    2. Documentez toutes les mesures correctives appliquées.

#### Comparaison des rapports

Après corrections, utilisez PingCastle pour évaluer l'amélioration de votre score de sécurité :

  - .\PingCastle.exe --compare-reports --report1 "report-20230601.xml" --report2 "report-20230701.xml"

### Automatisation

#### Création d'un script PowerShell

Automatisez l'exécution de plusieurs analyses PingCastle avec envoi par email :

  - $date = Get-Date -Format "yyyyMMdd"
  - $reportPath = "C:\Rapports\PingCastle\$date"

# Création du répertoire si nécessaire
if (-not (Test-Path $reportPath)) {
    New-Item -ItemType Directory -Path $reportPath
}

# Exécution de PingCastle avec plusieurs analyses

  - Start-Process -FilePath "C:\PingCastle\PingCastle.exe" -ArgumentList "--healthcheck --report-dir `"$reportPath`"" -Wait
  - Start-Process -FilePath "C:\PingCastle\PingCastle.exe" -ArgumentList "--graph --report-dir `"$reportPath`"" -Wait

# Notification par email
  
  - Send-MailMessage -To "securite@entreprise.com" -Subject "Rapport PingCastle $date" -Body "Les rapports sont disponibles à $reportPath"

## Ressources

https://www.pingcastle.com/
https://www.pingcastle.com/documentation/



# Analyse Screen

![Proxmox ping](https://github.com/user-attachments/assets/e9dcdc11-9a92-4224-9564-b9e0647c9d89)
----

![Proxmox ping1](https://github.com/user-attachments/assets/3670a351-849a-4481-ac40-e2fc023f676a)
----

![Proxmox ping2](https://github.com/user-attachments/assets/ce879871-c7b3-4ea2-b49a-fdc5fcc69bc2)
----

![Proxmox ping3](https://github.com/user-attachments/assets/ca6ee8f1-d188-4d49-94dc-3bdb2ccf8685)
----


