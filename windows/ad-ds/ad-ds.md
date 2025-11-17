---
title: Récapitulatif - AD DS
parent: Documentation AD DS
nav_order: 1
---

# Active Directory Domain Services (AD DS) - Documentation Technique

## 1. Présentation de l’architecture

Description rapide de l’infrastructure :  
- Nombre de contrôleurs de domaine : **2** 
- Version de Windows Server utilisée : **2022** 
- Domaine créé : **homelab.local**

---

## 2. Installation et configuration initiale

### Installation du rôle AD DS

1. Ouvrir le **Gestionnaire de serveur** (Server Manager).
2. Cliquer sur **Ajouter des rôles et fonctionnalités**.
3. Dans l’Assistant, cliquer sur **Suivant** jusqu’à atteindre la page **Sélection du rôle de serveur**.
4. Cocher la case **Services de domaine Active Directory (AD DS)**.
5. Cliquer sur **Suivant** puis sur **Installer**.
6. Attendre la fin de l’installation.

👉 [**Procédure**](./adds-installation.md)

### Promotion du serveur en contrôleur de domaine

1. Dans le **Gestionnaire de serveur**, une notification apparaît dans le coin supérieur droit indiquant que la configuration d’AD DS est requise.
2. Cliquer sur la notification puis sur **Promouvoir ce serveur en contrôleur de domaine**.
3. Choisir **Ajouter une nouvelle forêt** (si c’est une nouvelle infrastructure) ou **Ajouter un contrôleur de domaine à un domaine existant**.
4. Saisir le nom du domaine racine (exemple : **Homelab.local**).
5. Définir les options de niveau fonctionnel du domaine et de la forêt (par défaut Windows Server 2016/2019 selon version).
6. Configurer le mot de passe du mode restauration des services d’annuaire (DSRM).
7. Continuer en validant les options par défaut, ou adapter si nécessaire (DNS, chemin des bases de données…).
8. Lancer la promotion et redémarrer le serveur automatiquement à la fin.

👉 [**Procédure**](./dc-promtion.md)

---

## 3. Création des Unités d’Organisation (OU)

Description de la structure des OU mises en place (exemple) :
```
homelab.local
├── Utilisateurs
├── Groupes
├── Ordinateurs
└── Services
```

### Capture d’écran
![Création OU](./captures/ou_creation.png)

---

## 4. Gestion des utilisateurs et groupes

### 4.1 Création d’un utilisateur

- Étapes suivies pour créer un utilisateur.

### Capture d’écran  
![Création utilisateur](./captures/user_creation.png)

### 4.2 Gestion des groupes

- Création et affectation d’utilisateurs à des groupes.

### Capture d’écran  
![Gestion groupes](./captures/group_management.png)

---

## 5. Application des Group Policy Objects (GPO)

- Description simple de la GPO créée (exemple : redirection de dossiers, sécurité)

### Capture d’écran  
![GPO](./captures/gpo_configuration.png)

---

## 6. Tests et validation

- Explication rapide des tests d’authentification, de jonction au domaine, etc.

---

## Annexes

- Liens vers les ressources utilisées  
- Commandes Powershell ou scripts utilisés (si applicable)
