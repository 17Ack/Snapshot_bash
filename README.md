# Proxmox Auto-Snap Manager
Proxmox Auto-Snap est une solution d'automatisation légère en Bash pour gérer la planification de snapshots sur vos machines virtuelles Proxmox VE. Il permet de classer vos VMs par niveau de criticité et automatise l'inscription dans le crontab.

## Fonctionnalités
Provisionnement Automatique : Le script configure son propre environnement au premier lancement.

## Prérequis
Un serveur Proxmox VE installé.

Accès utilisateur Root ou privilèges Sudo.

Utilitaire column (généralement présent par défaut) pour l'affichage des listes.

Configuration Cron générée
Le script installe automatiquement les règles suivantes dans votre crontab :

3 Niveaux de Rétention :

Mensuel (Pas critique) : Planifié le 1er de chaque mois à 02h00.

Journalier : Planifié chaque nuit à 03h00.

Critique : Planifié toutes les 30 minutes.

Interface Menu : Utilisation interactive simple pour ajouter des VMs sans toucher à la syntaxe Cron.

Sécurité : Vérification des privilèges Root et détection des doublons pour éviter de surcharger les tâches.

Moteur Dynamique : Génère des snapshots horodatés automatiquement (nom_YMD-HMS).

 Architecture du Projet
Le script organise ses composants dans /opt/proxmox-auto-snap :

snapshot_PC.sh : Script exécuté mensuellement.

snapshot_J.sh : Script exécuté quotidiennement.

snapshot_C.sh : Script exécuté toutes les 30 minutes.

commande_snapshot.sh : Le moteur qui injecte les commandes dans les fichiers cibles.

# Installation
Bash

### 1. Cloner le dépôt
git clone [ici](https://github.com/17Ack/Snapshot_bash.git)

### 2. Se déplacer dans le dossier
cd proxmox-auto-snap

### 3. Rendre le script exécutable
chmod +x manager.sh

### 4. Lancer le script (nécessite les droits root)
sudo ./manager.sh
 Utilisation
Lancer le menu : sudo ./manager.sh

Option 1 : Entrez le VMID de votre machine (le script listera les VMs disponibles).

Choisir le niveau : Sélectionnez 1, 2 ou 3 selon l'importance de la VM.

Nommer : Donnez un nom et une description. Le script s'occupe de l'horodatage.

Vérifier : Utilisez l'Option 2 du menu pour voir vos tâches planifiées actuelles.

Prérequis
Un serveur Proxmox VE installé.

Accès utilisateur Root ou privilèges Sudo.

Utilitaire column (généralement présent par défaut) pour l'affichage des listes.

Configuration Cron générée
Le script installe automatiquement les règles suivantes dans votre crontab :

Bash

0 2 1 * * /opt/proxmox-auto-snap/snapshot_PC.sh  # Mensuel

0 3 * * * /opt/proxmox-auto-snap/snapshot_J.sh   # Journalier

*/30 * * * * /opt/proxmox-auto-snap/snapshot_C.sh   # Critique

 Avertissement
La fonctionnalité de suppression est actuellement en cours de développement (Option 3). Veillez à vérifier manuellement votre stockage pour éviter la saturation due à l'accumulation de snapshots.

Licence
Distribué sous la licence MIT. Voir LICENSE pour plus d'informations.

Auteur : 17Ack
