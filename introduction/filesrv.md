---
title: Serveur de fichier
parent: Introduction
nav_order: 4
---

# Introduction au Serveur de Fichiers
---

## 🎯 Objectif de la page
Présenter de manière claire et professionnelle :
- le rôle d’un serveur de fichiers dans une infrastructure d’entreprise,
- les concepts essentiels (NTFS, partage SMB, droits, héritage, quotas…),
- les bonnes pratiques d’administration,
- et les tâches que j’ai déjà réalisées dans le cadre de mon portfolio.

---

# 📁 Qu’est-ce qu’un serveur de fichiers ?

Un **serveur de fichiers** est un serveur dédié au stockage, au partage et à la gestion des données d’une organisation.  
Il permet aux utilisateurs d’accéder à des dossiers partagés de manière sécurisée, centralisée et organisée.

Le File Server sous Windows utilise principalement :
- le protocole **SMB** (Server Message Block),
- les permissions **NTFS**,
- les stratégies **Share Permissions**,
- les fonctionnalités avancées comme les **quotas**, **DFS**, **Shadow Copies**, etc.

### Pourquoi un serveur de fichiers est indispensable ?
- Centralisation et sécurisation des données.  
- Gestion fine des droits d’accès.  
- Sauvegarde et restauration facilitées.  
- Collaboration interne structurée.  
- Contrôle total sur les accès et modifications.

---

# 🧱 Concepts clés d’un serveur de fichiers

### 📌 Permissions NTFS
Les permissions NTFS permettent de contrôler l’accès localement au système de fichiers.

Principaux niveaux :
- **Read**  
- **Write**  
- **Modify**  
- **Full Control**

Propriétés importantes :
- Permissions **granulaires**,  
- Héritage activable/désactivable,  
- Contrôle fin via l’**ACL** et les **ACE**.

### 📌 Permissions de partage (Share Permissions)
S’appliquent au niveau du partage SMB.

Niveaux classiques :
- **Read**  
- **Change**  
- **Full Control**

💡 **Règle d’or :**  
> Les permissions effectives = le plus restrictif entre Share Permissions et NTFS.

### 📌 Structure recommandée pour les dossiers partagés
```
D:\Services
├── COMMUN
├── IT
├── RH
├── FINANCE
└── UTILISATEURS
    ├── user1
    ├── user2
    └── user3
```

### 📌 Quotas (FSRM)
Permettent de limiter l’espace disque par utilisateur ou par dossier.

Types de quotas :
- Quotas durs (bloquants)
- Quotas souples (non bloquants, alertes)

### 📌 Shadow Copies
Permet la restauration de versions précédentes d’un fichier ou dossier.

---

# 🔐 Rôle du serveur de fichiers dans un environnement AD

Dans une infrastructure Active Directory, le serveur de fichiers garantit :
- l’accès contrôlé aux dossiers selon les groupes AD,
- la gestion centralisée des profils utilisateurs,
- la mise en place de redirections de dossiers (Documents, Bureau…),
- la gestion des dossiers communs de service,
- le stockage organisés des données métier.

Serveur de fichiers + AD =  
➡️ gestion des droits cohérente  
➡️ administration simplifiée  
➡️ sécurité accrue

---

# 🛠️ Bonnes pratiques pour un serveur de fichiers

✔️ **Utiliser la méthode AGDLP** pour une gestion propre des permissions.  
✔️ **Séparer Share Permissions (large) et NTFS (restrictif)** pour une administration claire.  
✔️ **Désactiver l’héritage** dans les dossiers sensibles (RH, utilisateurs…).  
✔️ **Créer une structure de dossiers claire** et documentée.  
✔️ **Activer Shadow Copies** pour permettre aux utilisateurs de restaurer leurs fichiers.  
✔️ **Mettre en place FSRM** (quotas + filtrage de fichiers).  
✔️ **Éviter de donner Full Control aux utilisateurs**, sauf cas exceptionnels.  
✔️ **Sécuriser les partages administratifs** et désactiver les anciens protocoles SMB (1.0).  
✔️ **Sauvegarder régulièrement les données** (Veeam, Windows Server Backup…).  

---

# 📑 Ce que j’ai déjà réalisé (Portfolio)

### 🔧 Travaux effectués sur serveur de fichiers Windows Server

✔️ Création d’une arborescence professionnelle de dossiers partagés.  
✔️ Mise en place de partages SMB avec permissions NTFS détaillées.  
✔️ Configuration des droits via la méthode **AGDLP**.  
✔️ Création et gestion de quotas via **FSRM**.  
✔️ Mise en place de dossiers utilisateurs (Home Folders).  
✔️ Gestion des redirections de dossiers via GPO.  
✔️ Vérification des permissions effectives avec `Effective Access`.  
✔️ Tests d’accès via comptes utilisateurs de test.  
✔️ Documentation de la structure et des droits appliqués.

---
