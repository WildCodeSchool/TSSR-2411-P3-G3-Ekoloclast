# Installation du RODC sur le Windows Core

## ***Installation de l'Active Directory:***

L'étape suivante consiste à installer le rôle Active Directory Domain Services (ADDS). Pour ce faire, exécutez la commande suivante dans la console PowerShell :

     - Install-WindowsFeature AD-Domain-Services –IncludeManagementTools -Verbose
 
S'assurer que le role à bien été installé :

     - Get-WindowsFeature -Name *AD*

