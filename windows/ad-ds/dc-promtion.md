---
title: Procédure - Promotion DC
parent: Documentation AD DS
nav_order: 4
---

# 📘 Promotion du serveur en contrôleur de domaine (AD DS)

---

Cette procédure décrit la promotion d’un serveur Windows en contrôleur de domaine via l’interface graphique.  

---

## 1. Ouvrir la notification AD DS

Une fois le rôle AD DS installé, une notification apparaît en haut à droite du **Gestionnaire de serveur**.

1. Cliquer sur l’icône de notification.
2. Sélectionner **Promouvoir ce serveur en contrôleur de domaine**.

**Capture d’écran :**  
![Notification promotion AD DS](/admin-homelab/assets/capture/adds/01_promo_notification.png)

---

## 2. Choisir le type de déploiement

Dans l’Assistant Configuration des Services de domaine Active Directory :

1. Choisir l’option adaptée :
   - **Ajouter une nouvelle forêt** (cas le plus courant dans un homelab)
   - ou **Ajouter un contrôleur de domaine à un domaine existant**.

2. Si nouvelle forêt : entrer le nom du domaine, par ex. :  
   `entreprise.local`.

**Capture d’écran :**  
![Choix du type de déploiement](/admin-homelab/assets/capture/adds/02_deployment_type.png)

---

## 3. Configurer les options du contrôleur de domaine

1. Choisir les **services à installer** sur le contrôleur de domaine :
   - DNS Server (souvent recommandé)
   - Global Catalog (activé par défaut)
2. Définir le **mot de passe DSRM** (obligatoire).

**Capture d’écran :**  
![Configuration DC](/admin-homelab/assets/capture/adds/03_dc_options.png)

---

## 4. Options DNS

Une fenêtre peut indiquer que la délégation DNS ne peut pas être créée.  
Cela est normal dans une nouvelle forêt.

1. Cliquer simplement sur **Suivant**.

**Capture d’écran :**  
![Options DNS](/admin-homelab/assets/capture/adds/04_dns_options.png)

---

## 5. Chemins des dossiers AD DS

Laisser généralement les valeurs par défaut :

- Base de données AD  
- Journaux  
- SYSVOL

ou adapter si politique interne.

**Capture d’écran :**  
![Chemins AD DS](/admin-homelab/assets/capture/adds/05_paths.png)

---

## 6. Vérification de la configuration

L’assistant lance une **vérification de la configuration**.

1. S’assurer qu’aucune erreur critique n’est présente.  
2. Cliquer sur **Installer**.

**Capture d’écran :**  
![Vérification](/admin-homelab/assets/capture/adds/06_prereq_check.png)

---

## 7. Installation et redémarrage

Le serveur est automatiquement promu en contrôleur de domaine.  
Une fois l’installation terminée, il redémarre.

**Capture d’écran :**  
![Installation DC](/admin-homelab/assets/capture/adds/07_installation.png)

---

## Étape suivante

➡️ Procéder à la création des **OU**, **utilisateurs**, **groupes** et à la configuration des **GPO**.

Une page dédiée détaillera ces étapes.

---
