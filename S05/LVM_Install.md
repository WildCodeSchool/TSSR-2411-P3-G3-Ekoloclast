## STOCKAGE AVANCÉ - Mettre en place LVM sur un serveur Debian

### **Introduction**

LVM (Logical Volume Manager) permet la création et la gestion de volumes logiques sous Linux. L'utilisation de volumes logiques remplace en quelque sorte le partitionnement des disques. C'est un système beaucoup plus souple, qui permet par exemple de diminuer la taille d'un système de fichier pour pouvoir en agrandir un autre, sans se préoccuper de leur emplacement sur le disque

---
### 1) Ajouter un disque supplémentaire sur la VM Debian (ne pas démarrer la VM)

Faire un simple click sur la VM pour accéder à la configuration dans le panneau à droite.

Aller dans hardware/ Add / Hard disk dans "storage" sélectionner local-datas et cliquer sur add.

![lvm1](https://github.com/user-attachments/assets/741fdf44-e45d-4c78-8cb1-de9ea33b9e74)

Démarrer la VM debian

---
### 2) Configuration de LVM

Vérifier si LVM est déjà installé avec la commande **"sudo lvm version"**

Si ce n'est pas le cas, il faut l'installer à l'aide de la commande **"sudo apt install lvm2"**

Identifier le disque  non-système avec la commande **fdisk -l** ce sera le /dev/sdb

Initialiser le disque pour l'utilisation de LVM avec la commande **sudo pvcreate /dev/sdb**

Créer un groupe de volume vg_datas avec la commande **"sudo vgcreate vg_data /dev/sdb"**

Vérifier avec la commande **"sudo vgdisplay"** que la création s'est bien passée

Créer un volume logique lv_datas de 32 Go avec la commande lvcreate sur la totalité du disque : **"sudo lvcreate -l 100%FREE -n lv_data vg_data"**

Avant de pouvoir utiliser un volume logique, il faut le formater avec un système de fichiers. Nous allons utiliser ext4 avec la commande :

**"sudo mkfs.ext4 /dev/vg_datas/lv_datas"**

Pour accéder aux données d'un volume logique, il faut le monter sur un répertoire. Nous allons créer le répertoire /mnt/datas et y monter le volume logique lv_datas à l'aide des commandes ci-dessous

**sudo mkdir /mnt/datas**

**mount /dev/vg_data/lv_data /mnt/datas**

Vérifier avec la commande **lsblk** que l'opération a réussi, on voit ci-dessous que sdb est bien configuré en sdb :

![lvm2](https://github.com/user-attachments/assets/4d9acf3f-e66f-4349-b97c-8fe0c73097aa)






