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
