# Mise en place et configuration d'un serveur Apache2

Voici les étapes générales à suivre pour permettre à un site web interne à l'entreprise et externe d'être accessible via un serveur Apache2.

---

## Prérequis :

- Une VM/un conteneur avec **Debian 12** installé en CLI.

---

## Vérifiez qu'Apache2 est installé :

Il faut s'assurer que le serveur Apache2 est installé et en cours d'exécution sur votre machine. Si ce n'est pas le cas, vous pouvez l'installer avec les commandes suivantes (sur une distribution Debian/Ubuntu) :

```bash
sudo apt update && sudo apt upgrade  
sudo apt install apache2
```

Une fois l'installation terminé, vérifier le status d'Apache2 et le démarré s'il n'est pas activé :

![image](https://github.com/user-attachments/assets/230a874d-6c5a-4992-b203-7270b9472ae8)

## Installer maintenant Bind9 pour permettre des résolutions DNS et le démarrer :

```bash
sudo apt install bind9
```
![image](https://github.com/user-attachments/assets/6132ebcd-441d-4924-bbf3-915fa0ded2c3)

## Configurer un site interne avec Apache2 :

**1. Modifier le fichier de configuration d'Apache2 (000-default.conf) :**
   
Trouver le fichier de configuration par défaut d'Apache2 :

![image](https://github.com/user-attachments/assets/de9c16c8-9938-460b-9a91-6d21849db0d1)

Ouvrir le fichier de configuration par défaut d'Apache2 :

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

Il faut à présent, modifier la directive VirtualHost pour qu'elle écoute uniquement sur l'adresse IP privée du serveur ou le réseau local, et non sur toutes les interfaces réseau.
Exemple de modification pour une adresse IP interne (dans notre cas, 172.24.10.50) :

<VirtualHost 172.24.10.50:80><br>
    ServerAdmin admin@localhost<br>
    DocumentRoot /var/www/html<br>
    ErrorLog ${APACHE_LOG_DIR}/error.log<br>
    CustomLog ${APACHE_LOG_DIR}/access.log combined<br>
</VirtualHost>

![image](https://github.com/user-attachments/assets/1deb6ce2-76fa-413f-9678-7c56bfb20578)

Il faut s'assurer que le serveur Apache écoute uniquement sur l'IP du réseau local, afin que personne n'accède au site depuis l'extérieur.

**2. Ajouter des éléments sur le site interne**
   
Une fois que le interne est configuré, il faut ajouter des éléments au site. Pour cela, il est possible de:

•	Ajouter ou modifier des fichiers HTML, CSS, JavaScript, etc.<br>
•	Modifier des fichiers de contenu dynamiques (par exemple, PHP, Python).<br>
•	Ajouter des images, des vidéos, des formulaires ou toute autre ressource nécessaire à votre site.<br>

Tous les changements sont effectués directement dans le répertoire du site (/var/www/html) mentionné sur la ligne "DocumentRoot" du fichier de config :

![image](https://github.com/user-attachments/assets/cf158ca1-7be3-4eb2-9b8f-4f9beda2329f)

Le .html permet d'ajouter du contenu à la page.  
Pour améliorer la mise en forme on peut avoir également des fichiers .CSS. 

On va donc éditer index.html pour ajouter le contenu voulu à notre page web interne :

![image](https://github.com/user-attachments/assets/3ca75067-d43e-44b7-b08d-7e87871be794)

**3. Redémarrer Apache pour appliquer les changements**
   
```bash  
sudo systemctl restart apache2
```

**4. Accéder au site interne**
   
Maintenant que le site est configuré pour être accessible uniquement à l'intérieur de notre réseau local, on peut y accéder via l'adresse IP interne de notre serveur.

Ouvrir un navigateur sur un autre appareil de réseau et accéder à :

http://172.24.10.50

A savoir : Si vous avez configuré un nom de domaine local (par exemple, monsite.local), vous pouvez également y accéder en utilisant ce nom (assurez-vous que le domaine est bien résolu dans votre réseau local, soit via le fichier hosts, soit via un serveur DNS interne).

![image](https://github.com/user-attachments/assets/036f16d3-2262-4370-b95e-9725b4b82062)

Vous avez maintenant désormais accès à votre site web interne de votre entreprise. Il ets également accessible sur tous les apapreils connecté à votre réseau.

## Configurer un site externe avec Apache2 :

On va maintenant créer un site qui sera disponible à tous les réseaux avec un nom de domaine gratuit et une IPV6<br>
Les étapes de configuration sont similaires que le site interne avec quelques différences.

## Prérequis:

- Avoir une carte réseau en IPV6 sur la VM

  
## Créer le dossier pour le site web :

Une fois les serveurs installés, créer un dossier dans lequel vous allez stocker les fichiers de votre site web. Par exemple, vous pouvez créer un dossier monsite dans /var/www/ :

```bash
sudo mkdir /var/www/monsite
```

![image](https://github.com/user-attachments/assets/0e930ed2-6dc7-4179-ba97-6279a072f214)

Ajoutez vos fichiers web dans ce dossier :
Copiez vos fichiers HTML, CSS, JavaScript, images, etc., dans le dossier /var/www/monsite.

![image](https://github.com/user-attachments/assets/34b15cc8-6712-4e2f-aeae-961d8013cd04)

```bash
sudo cp -r /chemin/vers/mes/fichiers/* /var/www/monsite/
```
Pour pouvoir accéder à notre site par son nom de domaine, il faut soit en payer un, soit en générer un gratuitement sur des sites en ligne comme https://www.duckdns.org/ en rentrant son adresse IPV6.

![image](https://github.com/user-attachments/assets/90baae62-1c87-40dd-adee-e802f12711be)

Une fois l'adresse créé, il faut ajouter le nom de domaine du site dans un nouveau fichier de configuration.

## Créer un fichier de configuration pour le site :

Retourner dans /etc/apache2/sites-available/. 

Créer le fichier de configuration du site monsite.conf :

```bash
sudo touch monsite.conf
```

![image](https://github.com/user-attachments/assets/3dcf3688-4b2d-4248-bf6c-a3a15c4a9d16)

On va à présent l'éditer :

```bash
sudo nano /etc/apache2/sites-available/monsite.conf
```
Ajouter la configuration suivante avec le nom de domaine que vous avez généré (dans notre cas, monsite.com = ekoloclast.duckdns.org):

<VirtualHost *:80><br>
    ServerAdmin admin@monsite.com<br>
    ServerName monsite.com<br>
    DocumentRoot /var/www/monsite<br>
    ErrorLog ${APACHE_LOG_DIR}/error.log<br>
    CustomLog ${APACHE_LOG_DIR}/access.log combined<br>
</VirtualHost><br>

o	ServerAdmin: L'adresse e-mail de l'administrateur du site.<br>
o	ServerName: Le nom de domaine de votre site.<br>
o	DocumentRoot: Le chemin vers le dossier contenant vos fichiers du site.<br>

![image](https://github.com/user-attachments/assets/98e288a4-9666-4217-8819-8ef7205a7bc0)

## Activez votre site et redémarer apache2 :

Utilisez la commande a2ensite pour activer la configuration du site :

```bash
sudo a2ensite monsite.conf
sudo systemtcl restart apache2
sudo systemctl reload apache2
```
## Vérifier que le serveur est accessible :

Maintenant, vous devriez pouvoir accéder au site en ouvrant un navigateur et en saisissant l'adresse de votre domaine (dans notre cas, http://ekolcolast.duckdns.org).

![image](https://github.com/user-attachments/assets/009ae9e4-cc70-4489-af6e-a9b2ad33f408)


