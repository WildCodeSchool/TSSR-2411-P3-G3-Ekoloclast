# Analyser des scripts avec le module PSScriptAnalyzer

---


**1) Ouvrir Powershell**
---
![psscript1](https://github.com/user-attachments/assets/f09d66d0-1b3b-4920-85ed-5b97304edeb7)

**2) Installer le module PSScriptAnalyzer**
---
![psscript2](https://github.com/user-attachments/assets/26145a19-4b8c-4d01-8289-4773b6ab8d70)

**3) Analyser un script avec PSScriptAnalyser**
---
Exécuter la commande ci-dessous en spécifiant le chemin du script à analyser

![psscript3](https://github.com/user-attachments/assets/5b4d52aa-bf3a-464a-9603-45b3856e86d6)

**4) La commande retourne deux messages :**
---
L'utilisation d'un alias sur la ligne 2. En effet, "ls" est un alias de "Get-ChildItem", ce qui n'est pas recommandé.

La présence d'espace à la fin de la ligne 6. En effet, il y a des espaces à la suite de la commande "Write-Output".

**5) Suite à ce retour on peut modifier le script en corrigeant les erreurs relevées :**
---
![psscript4](https://github.com/user-attachments/assets/3ecb8efa-b650-417a-ac85-812f1b78e7ca)


**6) On teste le script à nouveau et on s'aperçoit que les erreurs ont disparu**
---
![psscript5](https://github.com/user-attachments/assets/53202c96-8c13-44c9-bd03-06141a84ceb1)

**7) PSScriptAnalyzer dans visual studio code**
---
PSScriptAnalyzer est pris en charge nativement dans Visual Studio Code. Ainsi, si nous utilisons un alias dans un script, ce dernier est immédiatement mis en évidence et VSCode, par l'intermédiaire de PSScriptAnalyzer, nous indique qu'il est déconseillé d'utiliser un alias. 

![psscript6](https://github.com/user-attachments/assets/f651650e-a26e-4770-91e1-35a8ec2b81ba)

