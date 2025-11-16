---
title: DNS
parent: Introduction
nav_order: 2
---

# Introduction au DNS

---

## 🎯 Objectif de la page
Présenter de manière claire et professionnelle :
- le fonctionnement général du DNS,
- son rôle indispensable dans Active Directory,
- les bonnes pratiques d'administration,
- et les tâches déjà réalisées dans le cadre de mon portfolio.

---

# 🌐 Qu’est-ce que le DNS ?

Le **Domain Name System (DNS)** est un service réseau qui traduit un **nom de domaine** (lisible par un humain) en **adresse IP** (comprise par une machine).  
Il fonctionne comme un annuaire distribué, indispensable à la navigation et à l’accès aux services.

Exemples :  
- `www.google.com` → `142.250.75.206`  
- `serveur-fichiers.local` → `192.168.1.20`

### Pourquoi DNS est indispensable ?
- Permet d'accéder aux services réseau sans retenir leurs adresses IP.  
- Centralise et organise la gestion des noms d’hôtes.  
- Facilite la découverte automatique des ressources sur le réseau.  
- Constitue une brique essentielle pour de nombreux services (web, messagerie, Active Directory…).

---

## 📌 Rôle du DNS en environnement AD DS

Dans une infrastructure Active Directory, **DNS est un composant obligatoire**.  
Il permet aux postes clients, serveurs et contrôleurs de domaine de localiser les services critiques tels que :

- les contrôleurs de domaine (DC),
- les services Kerberos et LDAP,
- le Global Catalog,
- les services de réplication AD DS.

Active Directory s’appuie principalement sur des enregistrements DNS de type **SRV** pour :

- localiser automatiquement les DC,
- assurer l’authentification,
- permettre la jonction au domaine,
- garantir la réplication entre contrôleurs de domaine.

Sans DNS fonctionnel :  
➡️ pas d’authentification,  
➡️ pas de GPO,  
➡️ impossibilité de se connecter au domaine.

---

## 🧱 Concepts clés du DNS

### 📌 Zone DNS
Une zone contient les enregistrements DNS d’un domaine.  
Exemples :  
- `entreprise.local` (zone principale)  
- `0.168.192.in-addr.arpa` (zone de résolution inversée)

### 📌 Types de zones dans AD
- **Primary Zone** (non AD-integrated, stockée localement)  
- **AD-integrated Zone** (stockée et répliquée dans Active Directory)  
- **Stub Zone** (informations minimales sur la zone maîtresse)  
- **Forward Lookup Zone** (résolution nom → IP)  
- **Reverse Lookup Zone** (résolution IP → nom)

### 📌 Types d’enregistrements courants

| Type     | Utilité                                        |
|:--------:|:-----------------------------------------------|
| **A**    | Associe un nom → adresse IPv4                  |
| **AAAA** | Associe un nom → adresse IPv6                  |
| **CNAME**| Alias d’un enregistrement existant             |
| **MX**   | Serveur de messagerie                          |
| **SRV**  | Localisation des services AD (LDAP, Kerberos…) |
| **PTR**  | Résolution inversée (IP → nom)                 |

---

## 🛠️ Bonnes pratiques DNS

✔️ **Utiliser des zones AD-integrated**  
➡️ Réplication automatique, sécurisée et intégrée dans Active Directory.

✔️ **Activer les mises à jour dynamiques (Secure Only)**  
➡️ Empêche les mises à jour non authentifiées et améliore la sécurité.

✔️ **Avoir au moins deux serveurs DNS (idéalement deux DC)**  
➡️ Garantit la haute disponibilité du service DNS et d’Active Directory.

✔️ **Ne jamais mettre un DNS externe dans la configuration IP d’un DC**  
➡️ Cela casse la résolution interne et peut empêcher l’authentification.

✔️ **Faire pointer tous les postes vers les DNS internes**  
➡️ Indispensable pour découvrir les services AD via les enregistrements SRV.

✔️ **Créer la zone inversée**  
➡️ Facilite le diagnostic, les outils réseau et certaines applications internes.
