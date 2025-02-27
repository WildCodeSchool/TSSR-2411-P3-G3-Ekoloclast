# Guide d'installation de volumes en RAID 1 sous Windows

Ce guide explique comment configurer un volume en RAID 1 sur un système Windows en utilisant le gestionnaire de disques. Un volume RAID 1 (miroir) crée une copie exacte de vos données sur deux disques pour une meilleure sécurité.

## Prérequis

- Deux disques durs ou SSD de capacité similaire.
- Un ordinateur sous Windows (version 7, 8, 10 ou 11).
- Les disques doivent être vierges ou avoir leurs données sauvegardées, car la création du RAID effacera leur contenu.

---

### Étape 1 : Ouvrir le Gestionnaire de disques

1. Cliquez sur le bouton **Démarrer** et tapez **"Gestion des disques"** dans la barre de recherche.
2. Sélectionnez **"Créer et formater des partitions de disque dur"**.

![1Gestion de disques_initialisation de disques](https://github.com/user-attachments/assets/1866c255-f425-48aa-a3d0-35c5081f4cf1)


---

### Étape 2 : Initialiser les disques (si nécessaire)

Si vos disques n'ont pas encore été initialisés, vous serez invité à les initialiser avant de pouvoir créer le RAID.

1. Faites un clic droit sur chaque disque non initialisé et choisissez **Initialiser le disque**.
2. Sélectionnez le style de partitionnement (GPT ou MBR) selon vos besoins.


---

### Étape 3 : Créer un volume miroir (RAID 1)

1. Faites un clic droit sur un espace non alloué sur l'un des disques et sélectionnez **Nouveau volume miroir**.
2. Suivez l'assistant de création de volume :
   - Sélectionnez les deux disques à utiliser pour le RAID 1.
   - Définissez la lettre de lecteur et le formatage (généralement NTFS).


![2Nouveau volume en mirroir](https://github.com/user-attachments/assets/ee7a21a9-d8c0-4efe-929c-f4a7626f1838)


![3Nouveau volume en mirroir_AJOUTER](https://github.com/user-attachments/assets/6690f1a6-c78e-49dd-bfff-75564930a649)

---

### Étape 4 : Vérifier l'intégration du RAID

Après avoir terminé l'assistant, Windows créera le volume RAID 1 et commencera à le formater. Cela peut prendre un certain temps.

1. Une fois le formatage terminé, vérifiez que le volume est listé dans le **Gestionnaire de disques** avec l'option **RAID 1** ou **Miroir**.
2. Le volume devrait maintenant être visible dans l'**Explorateur de fichiers**.

![6RAID1](https://github.com/user-attachments/assets/cfe109bd-cc04-4e33-b020-59a743472265)



![7Resultat](https://github.com/user-attachments/assets/bdc61729-d61c-4666-b1bc-60c7513d464d)

---

### Étape 5 : Finalisation et utilisation

Votre volume RAID 1 est maintenant configuré et prêt à l'emploi. Vous pouvez y accéder comme un disque normal dans l'Explorateur de fichiers. 
Vous avez maintenant configuré avec succès un volume RAID 1 sur votre système Windows. Ce RAID garantit une copie miroir de vos données pour plus de sécurité en cas de défaillance d'un disque.


---



