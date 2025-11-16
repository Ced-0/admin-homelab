---
title: DNS
parent: Introduction
nav_order: 2
---

# Introdution au DNS

---

## 🎯 Objectif de la page
Présenter de manière claire et professionnelle :
- le fonctionnement général du DNS,
- son rôle indispensable dans Active Directory,
- les bonnes pratiques d'administration,
- et les tâches déjà réalisées dans le cadre de mon portfolio.

---

# 🌐 Qu’est-ce que le DNS ?

Le **Domain Name System (DNS)** est un service réseau qui permet de traduire un **nom de domaine** (lisible par un humain) en **adresse IP** (comprise par une machine).  
Il fonctionne comme un annuaire distribué, essentiel à la navigation et à l’accès aux services.

Exemples :  
- `www.google.com` → `142.250.75.206`  
- `serveur-fichiers.local` → `192.168.1.20`

### Pourquoi DNS est indispensable ?
- Permet d'accéder aux services sans retenir les IP.  
- Centralise la gestion des noms d’hôtes.  
- Facilite la découverte automatique des ressources réseau.  
- Constitue une brique essentielle pour de nombreux services (web, mails, AD…).

---

## 📌 Rôle du DNS en environnement AD DS

Dans une infrastructure Active Directory, **DNS est obligatoire** :  
il permet aux clients, serveurs et contrôleurs de domaine de localiser les services essentiels (DC, Kerberos, LDAP…).

Active Directory utilise massivement des enregistrements DNS de type SRV pour :

- localiser les contrôleurs de domaine,
- identifier les services d’authentification,
- faciliter la connexion au domaine,
- permettre la réplication AD DS.

Sans DNS → pas d’authentification, pas de GPO, pas de logon au domaine.

---

## 🧱 Concepts clés du DNS

### **Zone DNS**
Une zone contient les enregistrements DNS d’un domaine.  
Exemple :  
- `entreprise.local` (zone principale)
- `0.168.192.in-addr.arpa` (zone de résolution inversée)

### **Types de zones dans AD**
- **Primary Zone** (non AD–integrated)
- **AD-integrated Zone** (répliquée entre DC)
- **Stub Zone**
- **Forward Lookup Zone**
- **Reverse Lookup Zone**

### **Types d’enregistrements courants**

| Type     | Utilité                                        |
|:--------:|:-----------------------------------------------|
| **A**    | Associe un nom → adresse IPv4                  |
| **AAAA** | Associe un nom → adresse IPv6                  |
| **CNAME**| Alias (redirection interne)                    |
| **MX**   | Détermine le serveur de messagerie             |
| **SRV**  | Service AD : LDAP, Kerberos                    |
| **PTR**  | Résolution inversée (IP → nom)                 |

---
