---
title: Serveur de fichier
parent: Introduction
nav_order: 4
---

# 📁 Qu’est-ce qu’un serveur de fichiers ?

---

Un **serveur de fichiers** est un serveur dédié au stockage, au partage et à la gestion des données d’une organisation.  
Il permet aux utilisateurs d’accéder à des dossiers partagés de manière sécurisée, centralisée et organisée.

---

## Serveur de fichiers sous Windows Server

- Utilise principalement le protocole **SMB (Server Message Block)**.  
- Gestion des droits via les **permissions NTFS** et les **partages SMB**.  
- Fonctionnalités avancées : **quotas (FSRM)**, **Shadow Copies**, **redirections de dossiers**, etc.  
- Intégration avec Active Directory pour gérer les accès selon les groupes et utilisateurs.  
- Méthode recommandée pour les permissions : **AGDLP** (Ajouter à un Groupe, Groupe à un Domaine, etc.).

## Serveur de fichiers sous Linux (Debian)

- Utilise souvent **Samba** pour offrir des partages SMB/CIFS compatibles Windows.  
- Peut également proposer des partages **NFS** pour un environnement Linux/Unix natif.  
- Gestion des permissions basée sur les droits Linux classiques (chmod, chown) en complément de la configuration Samba.  
- Authentification des utilisateurs Samba liée aux utilisateurs Linux, avec gestion spécifique via `smbpasswd`.  
- Configuration principale dans `/etc/samba/smb.conf`.

---

# 🧱 Concepts clés d’un serveur de fichiers sous windows server

### 📌 Permissions de partage
S’appliquent au niveau du partage SMB.

Niveaux classiques :
- **Read**  
- **Change**  
- **Full Control**

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

### 🧩 Principe d’utilisation de la méthode AGDLP

C’est la méthode recommandée par Microsoft :
A → G → DL → P

| Type de groupe              | Contient                        | Utilisé pour                            |
| --------------------------- | ------------------------------- | --------------------------------------- |
| **A** : Accounts            | Utilisateurs                    | Comptes d’utilisateurs                  |
| **G** : Global Group        | Membres du même domaine         | Rôle ou fonction (ex : “Comptabilité”)  |
| **DL** : Domain Local Group | Groupes globaux ou universels   | Attribution des droits sur la ressource |
| **P** : Permissions         | Ressource (NTFS, partage, etc.) | Droits effectifs                        |

- Les utilisateurs sont membres d’un groupe global (GG).
- Les groupes globaux sont membres d’un groupe de domaine local (DL).
- Le DL reçoit les permissions sur la ressource.

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

## 🩺 Pourquoi un serveur de fichiers est indispensable ?
- Centralisation et sécurisation des données.  
- Gestion fine des droits d’accès.  
- Sauvegarde et restauration facilitées.  
- Collaboration interne structurée.  
- Contrôle total sur les accès et modifications.

---

# 📑 Ce que j’ai déjà réalisé (Portfolio)

### 🔧 Travaux effectués sur serveur de fichiers Windows Server

- Création d’une arborescence professionnelle de dossiers partagés.  
- Mise en place de partages SMB avec permissions NTFS détaillées.  
- Configuration des droits via la méthode **AGDLP**.  
- Création et gestion de quotas via **FSRM**.  
- Mise en place de dossiers utilisateurs (Home Folders).  
- Gestion des redirections de dossiers via GPO.  
- Vérification des permissions effectives avec `Effective Access`.  
- Tests d’accès via comptes utilisateurs de test.  
- Documentation de la structure et des droits appliqués.

---

# 🛠️ Bonnes pratiques pour un serveur de fichiers

**Utiliser la méthode AGDLP**
Gestion propre des permissions. 

**Séparer Share Permissions (large) et NTFS (restrictif)** 
Administration claire.  

**Désactiver l’héritage**
Dans les dossiers sensibles (RH, utilisateurs…).

**Créer une structure de dossiers claire**
Bien documentée.

**Activer Shadow Copies** 
Permettre aux utilisateurs de restaurer leurs fichiers. 

**Mettre en place FSRM**
(quotas + filtrage de fichiers).  

**Éviter de donner Full Control aux utilisateurs**
Sauf cas exceptionnels.  

**Sauvegarder régulièrement les données** 
(Veeam, Windows Server Backup…).  

---
