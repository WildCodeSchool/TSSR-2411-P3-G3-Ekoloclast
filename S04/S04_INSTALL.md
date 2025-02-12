# Installation et Configuration de pfSense en Ligne de Commande

## Prérequis

pfSense agissant comme un routeur, il est impératif d’avoir au moins **2 cartes réseaux** sur 2 réseaux différents :
- **WAN** (Internet)
- **LAN** (réseau local)

La première carte correspond à l’interface **WAN** et la seconde à l’interface **LAN**.



---

## 1. Installation de pfSense

### Étape 1 : Démarrer l’installation

1. Insérez l’ISO de pfSense dans la VM dédiée.
2. Démarrez la machine, le setup va se lancer automatiquement après quelques secondes.
3. L’installation se fait via le clavier : **Appuyez sur Entrée pour Accepter.**

### Étape 2 : Lancer l’installation

1. Vérifiez que vous êtes bien sur **"Install"** (sélectionné en bleu foncé).
2. **Appuyez sur Entrée** pour continuer.

### Étape 3 : Partitionnement du disque

1. Sélectionnez **Auto (ZFS)** ou **Auto (UFS)** selon votre besoin etet appuyez sur **Entrée**.
2. Sectionnez le disque qui vous est proposé en appuyant sur espace et confirmez en appuyant sur **Entrée**.
3. Confirmez l’effacement du disque en sélectionnant **Commit**.
6. L’installation démarre automatiquement (quelques secondes d’attente).

### Étape 4 : Finalisation

1. Une fois l’installation terminée, pfSense propose d’ouvrir un shell : sélectionnez **Reboot**.
2. Au redémarrage, pfSense teste et configure automatiquement les interfaces réseau.

---

## 2. Configuration en Ligne de Commande

### Vérification des Interfaces Réseau

Après le démarrage, pfSense affiche ses interfaces réseau :
- **WAN** : Adresse IP obtenue via DHCP ou aucune si l'adresse static n'a pas encore été définis.
- **LAN** : Adresse IP par défaut `192.168.1.1` (modifiable si on en veut une static).
- **Menu** : Un menu en CLI propose plusieurs options pour configurer le pfSense et les adresses IP.

### Configuration de l’Interface WAN

1. Tapez `2` puis `Entrée`.
2. Sélectionnez l’interface WAN (`2`).
3. À la question DHCP, répondez `n` (Non).
4. Saisissez l’adresse IP souhaitée (`10.0.0.5`).
5. Définissez le masque de sous-réseau en notation CIDR (ex: `29`).
6. Rentrez une passerrelle et répondez `n` pour l’IPv6.
7. Désactivez le serveur DHCP en répondant `n`.
8. Pour HTTPS, répondez `n` (si vous souhaitez le garder sécurisé).
9. L’IP de connexion à internet est désormais  `10.0.0.5`.

### Configuration de l’Interface LAN

1. Tapez `2` puis `Entrée`.
2. Sélectionnez l’interface LAN (`2`).
3. À la question DHCP, répondez `n` (Non).
4. Saisissez l’adresse IP souhaitée (`172.16.10.8`).
5. Définissez le masque de sous-réseau en notation CIDR (ex: `24`).
6. Laissez la passerelle vide et répondez `n` pour l’IPv6.
7. Désactivez le serveur DHCP en répondant `n`.
8. Pour HTTPS, répondez `n` (si vous souhaitez le garder sécurisé).
9. L’URL d’accès à pfSense est maintenant `https://172.16.10.8/`.

## 3. Accéder à l’Interface Web

1. Depuis un PC connecté au réseau local, ouvrez un navigateur.
2. Saisissez l’URL : `(https://172.16.10.8/)`.
3. Ignorez l’erreur de certificat (normale sur une installation locale).
4. Identifiants par défaut :
   - **Login** : `admin`
   - **Mot de passe** : `pfsense`
5. Cliquez sur `Next` pour lancer l’assistant de configuration.

## 4. Configuration Finale via l’Interface Web

### Étape 1 : Informations générales

1. Définissez un nom pour le firewall (facultatif).
2. Déclarez un serveur DNS.
3. Sélectionnez le fuseau horaire `Europe/Paris`.

### Étape 2 : Configuration WAN

1. Laissez en DHCP sauf si vous utilisez une IP fixe.
2. **PPPoE Configuration** : Ajoutez les identifiants de votre FAI si nécessaire.
3. Désactivez les règles bloquant les réseaux privés si vous êtes en environnement de test.

### Étape 3 : Configuration LAN

1. Vous pouvez modifier l’adresse IP du LAN si nécessaire (déjà configuré en ligne de commande).
2. Modifiez les identifiants par défaut de `admin`.

### Étape 4 : Finalisation

1. Cliquez sur `Reload` pour recharger pfSense.
2. Après rechargement, cliquez sur `Finish`.
3. Acceptez les conditions légales.

## 5. Tableau de Bord et Fonctionnalités

L’interface affiche :

- Utilisation des ressources
- Adresses IP configurées
- Mises à jour disponibles

**Actions possibles :**

- Ajouter des graphiques et logs
- Configurer des VPN (IPSEC, OpenVPN)
- Activer des services (DHCP, DNS, NTP…)
- Définir des règles de trafic
- Surveiller le trafic réseau
- Ajouter des plugins (ex: SquidGuard pour le filtrage web)

**Info + :** Pour changer la langue de pfSense, allez dans `System > General Setup`.

## Sécurité des Règles Firewall

- Par défaut, pfSense autorise tout le trafic :
  - Dans `Firewall > Rules > LAN`, tout protocole et adresse sont autorisés.
- Vous pouvez personnaliser ces règles pour restreindre les accès.

## Conclusion

Vous avez maintenant une installation fonctionnelle de pfSense, accessible via l’interface web, prête pour des configurations avancées.
