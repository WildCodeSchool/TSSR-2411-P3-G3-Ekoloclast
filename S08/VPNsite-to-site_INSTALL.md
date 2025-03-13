## VPN IPSEC

Un VPN site-to-site est un type de réseau privé virtuel qui permet de connecter de manière sécurisée plusieurs sites distants (comme des bureaux ou des succursales) via Internet ou un réseau privé. Contrairement à un VPN classique utilisé par un individu pour accéder à un réseau distant (VPN client-à-site), un VPN site-to-site relie directement les réseaux locaux (LAN) de chaque site comme s'ils faisaient partie du même réseau interne.

Nous allons utiliser **IPSec (Internet Protocol Security)** sur un pare-feu **pfSense**, qui est un ensemble de protocoles conçus pour assurer un transfert sécurisé des données sur un réseau. Il s'agit d'un standard ouvert fonctionnant au niveau de la **couche 3** du modèle OSI, prenant en charge plusieurs algorithmes de chiffrement et d'authentification pour garantir la confidentialité et l'intégrité des communications.

## Mise en place

Nous allons d'abord accéder à l'interface d'administration de notre premier **PfSense** (à mon adresse **172.24.10.12**). Une fois connectés, nous nous rendons dans le menu **"VPN"**, puis sélectionnons l'option **"IPsec"**.

![image](https://github.com/user-attachments/assets/c4219081-f32a-45b3-961e-d5caca6a8893)

### Configuration de la Phase 1

Une fois sur la page de configuration d'IPSEC, on clique sur **"+ Ajouter P1"** pour ajouter la phase 1 puis on va configurer la phase 1 :

![image](https://github.com/user-attachments/assets/2a7f3378-9099-4b73-9d40-c241edb3e9d6)


- **Key Exchange version 2** : Choisir "Auto" si l'autre pair ne supporte pas l'IKEv2.
- **Internet Protocol** : Sélectionner "IPv4".
- **Interface** : Choisir "WAN".
- **Remote Gateway** : Adresse IP publique du site distant (**10.0.0.6** dans notre cas).
- **Description** : Optionnelle.
- **Authentication Method** : Sélectionner "PSK" (clé pré-partagée).
- **My identifier** : "My IP address".
- **Peer identifier** : "Peer IP address".
- **Pre-Shared Key** : Clé pré-partagée générée par pfSense.
- **Encryption Algorithm** : Privilégier "AES256-GCM" ou "AES128-GCM" avec "SHA256".

Laisser les autres options par défaut et cliquer sur **"Sauvegarder"**.

![image](https://github.com/user-attachments/assets/2bc7180b-6af3-40a0-9015-4ddeeda7a98a)

![image](https://github.com/user-attachments/assets/74340962-10e2-43ff-80bf-e6ea0000a806)

![image](https://github.com/user-attachments/assets/79ae384c-d7e5-4651-ad24-b6bf9051a952)

![image](https://github.com/user-attachments/assets/7d916a48-3bcb-4e74-9712-277183ba0c8d)

![image](https://github.com/user-attachments/assets/47b59053-8e3a-45ad-bfc9-951a88694542)


### Configuration de la Phase 2

Sous la **Phase 1** qui est désormais visible, cliquer sur **"Afficher les entrées Phase 2"** puis sur **"Ajouter P2"**.

![image](https://github.com/user-attachments/assets/30c7abb2-ca88-4d88-9098-26bd0952e240)

- **Mode** : "Tunnel IPv4".
- **Local Network** : "LAN subnet".
- **NAT/BINAT translation** : "Aucun".
- **Remote Network** : Adresse IP du réseau distant (**172.10.0.1**).
- **Description** : Optionnelle.
- **Protocol** : "ESP".
- **Encryption Algorithms** : "AES256-GCM" ou "AES128-GCM".

Laisser les autres options par défaut et cliquer sur **"Sauvegarder"**.

![image](https://github.com/user-attachments/assets/a4c18bf5-84ed-4aa2-8874-3a8817a3d49e)

![image](https://github.com/user-attachments/assets/3edeb12e-1a97-40e7-8ba2-fc6aef33c0b6)

![image](https://github.com/user-attachments/assets/717b2078-c2a2-47ea-b2e9-5d92a568eff7)

Une fois ceci fait, cliquer sur **"Appliquer les modifications"**.

![image](https://github.com/user-attachments/assets/088f5b99-038e-4b49-a98f-90c7844a3a58)


### Règles IPSEC

Créer une règle pour autoriser le trafic entrant et sortant du VPN. Pour cela, aller dans **"Pare-feu" > "Règles"** puis cliquer sur **"IPSEC"**.

Ajouter une nouvelle règle et la configurer comme suit :

![image](https://github.com/user-attachments/assets/8e23ca3a-4c19-4854-860c-a4af3105dcd1)

![image](https://github.com/user-attachments/assets/ece2cd6e-cb2e-42b1-a9c1-28124d31cd00)

### Activation de la connexion VPN

Ces configurations doivent être répliquées sur le **pfSense** du site distant en copiant la clé générée par le premier site.

Une fois les deux sites configurés, activer la connexion VPN en allant dans **"État" > "IPSEC"**.

![image](https://github.com/user-attachments/assets/8184b5c6-6e54-496e-83aa-631698e42598)

Cliquer sur **"Connecter P1 and P2s"**.

![image](https://github.com/user-attachments/assets/27a7a417-cea7-4554-9d0e-2e461f0e7615)

La connexion est maintenant établie.

![image](https://github.com/user-attachments/assets/81692c5b-a5d0-42c7-87de-6a94ae5dc1c7)

Tester la connexion entre les deux sites avec un **ping**.


