# Iredmail

***iRedMail est une solution open-source permettant de déployer rapidement un serveur de messagerie complet sous Linux. Il regroupe plusieurs services essentiels comme Postfix (serveur SMTP), Dovecot (serveur IMAP/POP3), et Roundcube (webmail). Il prend en charge les protocoles de chiffrement (TLS, SSL) et inclut des fonctionnalités de sécurité avancées comme la protection anti-spam (SpamAssassin, Amavis) et l’authentification avec OpenLDAP ou MariaDB/PostgreSQL. Son installation automatisée simplifie la mise en place d’un serveur mail sécurisé et fiable, idéal pour les entreprises et les organisations souhaitant un contrôle total sur leurs communications électroniques.***

## Installation et configuration
---------
### Configuration de Windows Server (DNS)
---------
En premier temps, il faut configurer le service DNS dans Windows Server, en ajoutant des zones directes et en faisant de nouveaux enregistrements

![DP IRED DNS](https://github.com/user-attachments/assets/4caa6ff0-fe0c-4877-9a69-9e2cadca92bd)
---------
![DP IRED DNS2](https://github.com/user-attachments/assets/1ad7e22b-bb56-412d-8664-498f52458c74)
---------
![DP IRED DNS3](https://github.com/user-attachments/assets/1b97efac-9816-4423-b10a-c8e706a9e2b7)
---------
![dp ired dns4](https://github.com/user-attachments/assets/cc6bf68f-f5e1-45a4-b235-364bd9eeb996)
---------
![DP IRED DNS5](https://github.com/user-attachments/assets/11652c87-4aa4-4ae8-b2fd-78c3c1883dcf)
---------

Une fois que le server est configurer, il n'y a plus que le serveur Débian à configurer 

### Installation sur débian 

  - Mettre à jour votre serveur

![DP IRED](https://github.com/user-attachments/assets/566baa41-ff47-49d7-9bff-1c87d61946fc)
---------
  - Téléchargement du package de messagerie

 sudo wget https://github.com/iredmail/iRedMail/archive/refs/tags/1.7.2.tar.gz  
 --------

![DP IRED 2](https://github.com/user-attachments/assets/78e5ad63-3efa-4817-a16f-76c95278e4e7)
---------
  - Décompression du fichier

![DP IRED 3](https://github.com/user-attachments/assets/b1a4ff06-4afd-4ae6-af37-ea56845a89d6)
---------
  - taper la commande cd pour vous déplacer dans le fichier

cd iRedMail-1.7.2

Il ne faut surtout pas oublier, de mettre à jour les packets avec la commande suivante.

sudo apt update

Afin de lier l'adresse IP de votre serveur, vous devrez aller dans le fichier Hosts

sudo nano /etc/hosts

![DP IRED HOST](https://github.com/user-attachments/assets/e5349d16-a241-4854-ae9a-27cc3ae99001)
----------

Une fois que tout cela est fait, vous pouvez lancer votre script bash

sudo bash iRedMail.sh

Mis à part pour le mot de passe et l'adresse mail qui va vous être demandée laisser tout par défauts, je recommande quand même de prendre (MariaDB)

![DP IRED5](https://github.com/user-attachments/assets/1d01f81b-6c30-4650-bca3-53d954ee25e4)
----------
![DP IRED6](https://github.com/user-attachments/assets/94807b00-f07f-46b8-8350-987a5f461802)
----------
![DP IRED7](https://github.com/user-attachments/assets/8cc2e4c5-32d8-43a2-b485-ab1ba9a4c86c)
----------
![DP IRED8](https://github.com/user-attachments/assets/6f2e9b27-e1fd-4e3b-a618-d6f3baf67943)
----------
![DP IRED9](https://github.com/user-attachments/assets/e3e04725-d761-4077-8f19-51610525325a)
--------
![DP IRED10](https://github.com/user-attachments/assets/39282424-6d45-44a0-af37-d2a6e66a10f7)
-
![DP IRED11](https://github.com/user-attachments/assets/734ef1db-b340-48f6-bde4-5c56f74c6292)
-
  - Ajouter au réglages (SOGO)

![DP IRED12](https://github.com/user-attachments/assets/c84f409d-44d5-4b54-94d5-b1e59c234bbb)
-

Ici, l'installation va vous demander s'il peut utiliser le port 22 par défauts, faire oui pour les deux questions.

![DP IRED13](https://github.com/user-attachments/assets/0bb46399-5297-4555-bbc4-72b05d9815ab)
-
![DP IRED14](https://github.com/user-attachments/assets/f70fe788-c1cb-4431-842d-ab4472e1399d)
-
![DP IRED15](https://github.com/user-attachments/assets/caca4da6-bf87-4d5d-9e37-90104ba733c5)
-
![DP IRED16](https://github.com/user-attachments/assets/f74b419a-e1a4-49cd-a5b0-e2b7c9b84177)
-

L'installation est terminée, rendez-vous sur Internet avec l'adresse ip pour vérifier que cela est marcher, en toute logique la messagerie devrait s'afficher.

{ Si jamais la page ne s'affiche pas correctement } Voici les commandes à taper :

php -v

  - Cela affichera quelque chose comme :

PHP 8.1.12 (cli) (built: Oct 25 2022 12:45:00) ( NTS )

Copyright (c) The PHP Group

Zend Engine v4.1.12, Copyright (c) Zend Technologies


2️⃣ Mettre à jour PHP

La méthode dépend de ton système d'exploitation :

📌 Sous Debian / Ubuntu

Ajoute le PPA de ondrej/php (si ce n’est pas déjà fait) :

sudo apt update && sudo apt upgrade -y
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update

Installe la nouvelle version (par exemple, PHP 8.3) :

sudo apt install php8.3 -y

Vérifie la version installée :

php -v

Si nécessaire, modifie la version par défaut :

sudo update-alternatives --config php























