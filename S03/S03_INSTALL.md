# Installation du RODC sur le Windows Core

## ***Installation de l'Active Directory:***

***L'étape suivante consiste à installer le rôle Active Directory Domain Services (ADDS). Pour ce faire, exécutez la commande suivante dans la console PowerShell :***

     - Install-WindowsFeature AD-Domain-Services –IncludeManagementTools -Verbose
 
***S'assurer que le role à bien été installé :***

     - Get-WindowsFeature -Name *AD*

***Après avoir installé le rôle ADDS, vous pouvez utiliser les applets de commande du module ADDSDeployment pour déployer un nouveau domaine, une nouvelle forêt ou un contrôleur de domaine supplémentaire :***

     - Get-Command -Module ADDSDeployment

***Il existe trois scénarios possibles :***

***Installation d'une nouvelle forêt Active Directory :***

     - Install-ADDSForest -DomainName woshub.com -ForestMode Win2016 -DomainMode Win2016 -DomainNetbiosName WOSHUB -InstallDns:$true
               
     - L' Install-ADDSDomainapplet de commande permet de créer un nouveau domaine dans une forêt Active Directory existante
     
     - Install-ADDSDomainController– permet d’ ajouter un nouveau contrôleur de domaine (supplémentaire) à un domaine Active Directory existant

          - Add-ADDSReadOnlyDomainControllerAccount








**Changer le nom de domaine du PC Windows 10 (poste client)**


Prérequis : Dans la configuration IPv4, le DNS doit être celui du serveur ADDS soit 172.24.10.1


![ajout PC domaine prérequis](https://github.com/user-attachments/assets/85ce26ee-1452-439f-baa9-cebbbb527bf5)



1) Allez dans l'explorateur de fichiers 

2) Clique droit sur 'this pc"/properties

3) To rename this computer.... Cliquer sur Change


![ajout PC domaine](https://github.com/user-attachments/assets/292ef3d9-eb5d-41f4-ae7b-40620bd0079f)



4) Cocher Domaine et saisir Ekoloclast.lan


![ajout PC domaine ](https://github.com/user-attachments/assets/e872e768-b076-43f7-9fc6-7a2a8830a39a)



5) Saisir le nom "Administrateur" et le mot de passe "Azerty1*"


![ajout PC domaine 3](https://github.com/user-attachments/assets/fbe95e5c-eb59-42ae-83fe-6008bd1e11fa)


6) Un message s'affiche à l'écran pour valider l'accès du PC au nom de domaine


![ajout PC domaine 4](https://github.com/user-attachments/assets/9c531125-f0a7-4697-90f3-e3a77a052bcd)


7) Redémarrer le PC

