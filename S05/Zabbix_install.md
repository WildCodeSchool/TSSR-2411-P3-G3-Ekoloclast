# Installation et Configuration de Zabbix sur Debian 12

## I. Présentation

Zabbix est une solution de supervision puissante et flexible conçue pour surveiller les performances des systèmes, des réseaux et des applications.

Ce tutoriel détaille chaque étape nécessaire pour installer et configurer Zabbix sur Debian 12, en utilisant MariaDB comme base de données et Apache comme serveur web.

## II. Mettre à jour le système

Avant de commencer, assurez-vous que votre système est à jour :

```bash
sudo apt -y update && sudo apt upgrade && sudo apt full-upgrade && sudo apt autoclean && sudo apt clean
```

## III. Installer le serveur de base de données MariaDB

La base de données est un composant essentiel pour Zabbix, car elle stocke toutes les données de supervision. Nous utiliserons **MariaDB**, une alternative open source à MySQL.

Pour installer MariaDB, exécutez la commande suivante :

```bash
sudo apt install mariadb-server mariadb-client -y
```

Démarrez et activez MariaDB puis effectuez la sécurisation de base à l'aide du script "mysql_secure_installation" :

```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
```

Lors de l'exécution de "mysql_secure_installation", appuyez sur `y` à toutes les étapes sauf lorsque vous devez définir un mot de passe.

## IV. Ajouter le dépôt Zabbix

Pour obtenir la dernière version de Zabbix, vous devez ajouter son dépôt officiel à votre système.

```bash
wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest+debian12_all.deb
sudo dpkg -i zabbix-release_latest+debian12_all.deb
sudo apt update
```

## V. Installer Zabbix et ses dépendances

Procédez à l'installation des composants essentiels de Zabbix, notamment le serveur, l'agent et l'interface web :

```bash
sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent -y
```

## VI. Configurer la base de données pour Zabbix

Connectez-vous à MariaDB :

```bash
sudo mysql -u root -p
```

Créez une base de données dédiée pour Zabbix et configurez un utilisateur spécifique avec les commandes suivantes :

```sql
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'VotreMotDePasseZabbix';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
SET GLOBAL log_bin_trust_function_creators = 1;
EXIT;
```

Importez ensuite le schéma initial de Zabbix en utilisant le mot de passe de votre utilisateur "zabbix" :

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -uzabbix -p zabbix
```

Désactivez l'option `log_bin_trust_function_creators` :

```bash
sudo mysql -u root -p -e "SET GLOBAL log_bin_trust_function_creators = 0;"
```

## VII. Configurer Zabbix Server

Modifiez le fichier de configuration de Zabbix Server pour inclure les informations d'accès à la base de données :

```bash
sudo nano /etc/zabbix/zabbix_server.conf
```

Trouvez et modifiez les lignes suivantes :

```conf
DBPassword=VotreMotDePasseZabbix
EnableGlobalScripts=1
```

## VIII. Configurer Apache et PHP

Pour assurer le bon fonctionnement de l'interface web de Zabbix, il est nécessaire de configurer correctement PHP qui est géré par Apache.

Modifiez les paramètres de configuration de PHP :

```bash
sudo nano /etc/zabbix/apache.conf
```

Assurez-vous que le fuseau horaire est défini :

```conf
php_value date.timezone Europe/Paris
```

Enfin, redémarrez Apache pour appliquer les modifications :

```bash
sudo a2enmod php8.2
sudo systemctl restart apache2
sudo systemctl enable apache2
```

## IX. Configurer le Pare-feu

Pour sécuriser votre serveur, configurez le pare-feu pour n'autoriser que les ports nécessaires à Zabbix.

Ouvrez les ports pour les communications de Zabbix :

```bash
sudo apt install -y iptables
sudo iptables -A INPUT -p tcp --dport 10051 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 10050 -j ACCEPT
sudo mkdir -p /etc/iptables
sudo sh -c "iptables-save > /etc/iptables/rules.v4"
sudo iptables-restore < /etc/iptables/rules.v4
```

## X. Démarrer les services Zabbix

Une fois tous les composants installés et configurés, démarrez les services pour rendre Zabbix opérationnel.

Redémarrez et activez les services nécessaires :

```bash
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
```

## XI. Accéder à l'interface web de Zabbix

Pour finaliser la configuration, accédez à l'interface web de Zabbix en utilisant un navigateur.

Dans la barre d'adresse, saisissez :

```
http://<adresse_ip_serveur>/zabbix
