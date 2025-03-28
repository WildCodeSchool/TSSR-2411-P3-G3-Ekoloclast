# Audit des Serveurs Windows avec Sysinternals

## 1. **AccessChk** - Vérification du niveau d'accès d'un utilisateur

**But** : Cet outil permet de vérifier les droits d'accès d'un utilisateur ou d'un groupe sur un objet (dossier, fichier, clé de registre, etc.).

### Étapes :
1. **Téléchargement de Sysinternals** : A partir du site officiel [Microsoft Sysinternals](https://learn.microsoft.com/fr-fr/sysinternals/downloads/security-utilities).
   
2. **Exécution d'AccessChk** :
   - Ouvrir une invite de commandes **en tant qu’administrateur**.
   - Se rendre dans le répertoire où Sysinternals a été extrait.
   - Utiliser la commande suivante pour connaître les droits d’un utilisateur ou d’un groupe sur un dossier ou fichier spécifique :
     ```bash
     AccessChk.exe -d "C:\Chemin\Vers\Le\Dossier" 
     ```
     Remplacer `"C:\Chemin\Vers\Le\Dossier"` par le chemin réel de l’objet à auditer.
   
   ![Capture d’écran 2025-03-26 160009](https://github.com/user-attachments/assets/c9cd6575-0d70-45c7-8377-90d7d86b8fd2)

   - Il est aussi possible de spécifier un utilisateur ou un groupe pour vérifier ses droits :
     ```bash
     AccessChk.exe -u "NomUtilisateur" "C:\Chemin\Vers\Le\Dossier"
     ```
   - Cela permettra de lister les permissions de l'utilisateur spécifié sur les ressources ciblées.

## 2. **AccessEnum** - Audit des accès utilisateurs

**But** : Cet outil permet de scanner les fichiers, dossiers, clés de registre et autres objets afin de vérifier les autorisations et d’auditer les accès des utilisateurs.

### Étapes :
1. **Exécution d'AccessEnum** :
   - Lancer **AccessEnum.exe** depuis le répertoire où la suite Sysinternals a été extraite.
   - L'outil va scanner les ressources du serveur et afficher une liste des objets avec leurs permissions associées.
   - Il est possible de filtrer les résultats en sélectionnant les objets à auditer dans l’interface graphique.

![accessenum](https://github.com/user-attachments/assets/d8c8b143-f694-47b9-a96e-b7e7b74f291c)

2. **Analyse des résultats** :
   - Après le scan, analyser les résultats pour vérifier si des utilisateurs ou des groupes disposent de permissions excessives ou inappropriées sur des ressources sensibles.

![accessenum2](https://github.com/user-attachments/assets/bf576525-1482-4a01-9bd9-9c5a09c52c2d)

## 3. **ShareEnum** - Audit des partages de fichiers

**But** : ShareEnum permet d'examiner les partages réseau sur un serveur et de vérifier qui a accès à ces partages.

### Étapes :
1. **Exécution de ShareEnum** :
   - Lancer **ShareEnum.exe** depuis le répertoire de Sysinternals.
   - ShareEnum va scanner et lister tous les partages actifs sur le serveur.
   - Pour chaque partage, l’outil indiquera les utilisateurs ou groupes qui y ont accès, ainsi que le niveau de permission associé.

2. **Analyse des partages** :
   - Vérifier si des partages sensibles sont accessibles à des utilisateurs ou groupes non autorisés.
   - Si nécessaire, restreindre l'accès aux partages ou les désactiver.

## Conseils supplémentaires :
- **Automatisation** : Pour auditer plusieurs serveurs, il est possible d’automatiser l’exécution de ces outils avec des scripts batch ou PowerShell, permettant ainsi de les exécuter à distance sur d’autres machines.
- **Rapports** : Il est conseillé de rediriger les résultats des commandes vers des fichiers texte pour conserver une trace de l’audit. Par exemple :
   ```bash
   AccessChk.exe -d "C:\Chemin\Vers\Le\Dossier" > audit_accesschk.txt
