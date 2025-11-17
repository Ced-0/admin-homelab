---
title: Procédure - Installation AD DS
parent: Documentation AD DS
nav_order: 2
---

# 📘 Installation du rôle Active Directory Domain Services (AD DS)

---

Cette procédure décrit étape par étape l’installation du rôle **AD DS** via l’interface graphique de Windows Server.  

---

## 1. Ouvrir le Gestionnaire de serveur

1. Se connecter au serveur Windows.
2. Cliquer sur **Gestionnaire de serveur** (Server Manager) dans la barre des tâches ou le menu Démarrer.

**Capture d’écran :**  
![Gestionnaire de serveur](/admin-homelab/assets/capture/adds/01_server_manager.png)

---

## 2. Lancer l’assistant d’ajout de rôles

1. Dans le tableau de bord du Gestionnaire de serveur, cliquer sur **Ajouter des rôles et fonctionnalités**.

**Capture d’écran :**  
![Ajouter rôles](/assets/capture/adds/02_add_roles.png)

---

## 3. Parcourir l’assistant jusqu’à la sélection des rôles

1. Cliquer sur **Suivant** dans les pages :  
   - Avant de commencer  
   - Type d’installation  
   - Sélection du serveur  
2. Arriver sur la page **Sélection des rôles de serveur**.

**Capture d’écran :**  
![Assistant rôles](/assets/capture/adds/03_wizard_navigation.png)

---

## 4. Sélectionner le rôle AD DS

1. Cocher **Services de domaine Active Directory (AD DS)**.
2. Accepter l’ajout des fonctionnalités nécessaires si une fenêtre apparaît.

**Capture d’écran :**  
![Sélection AD DS](/assets/capture/adds/04_select_adds.png)

---

## 5. Installation du rôle

1. Cliquer sur **Suivant** jusqu’à la page de confirmation.
2. Cliquer sur **Installer**.

**Capture d’écran :**  
![Installation AD DS](/assets/capture/adds/05_install_adds.png)

---

## 6. Attendre la fin de l’installation

L’assistant installe les composants AD DS.  
Aucune action n’est requise jusqu’à la fin du processus.

**Capture d’écran :**  
![Fin installation](/assets/capture/adds/06_install_complete.png)

---

## Étape suivante

➡️ Une fois l’installation terminée, procéder à la **promotion du serveur en contrôleur de domaine**.

(La procédure sera détaillée dans une page dédiée.)

---
