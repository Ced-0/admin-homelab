---
title: "DNS - Introduction"
description: "Guide DNS en environnement Windows et Active Directory"
permalink: /introduction/dns/
weight: 2
---

# DNS sur Windows Server

## 🎯 Objectif de la page
Comprendre le rôle du DNS dans un environnement Active Directory, documenter sa configuration sous Windows Server et montrer des exemples concrets de tâches d’administration.

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

## 🏗️ Installation du rôle DNS (si non installé)

Le rôle DNS est automatiquement installé lors de la promotion en DC.  
Sinon :

```powershell
Install-WindowsFeature DNS -IncludeManagementTools
