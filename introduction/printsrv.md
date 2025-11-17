---
title: Serveur d'impression
parent: Introduction
nav_order: 5
---

# 🖨️ Qu’est-ce qu’un serveur d’impression ?

Un **serveur d’impression** centralise, gère et distribue les imprimantes au sein d’un réseau d’entreprise.  
Il permet aux utilisateurs d’accéder facilement aux imprimantes tout en garantissant une gestion contrôlée, sécurisée et centralisée.

## Serveur d’impression sous Windows permet :

- l’installation et le partage d’imprimantes,
- la gestion des files d’attente d’impression,
- le déploiement d’imprimantes via GPO,
- la gestion centralisée des pilotes d’impression,
- la surveillance des impressions et des incidents.

## Serveur d’impression sous Linux utilise principalement **CUPS** (Common Unix Printing System) et permet :
- l’installation et le partage d’imprimantes,
- la gestion des files d’attente d’impression,
- la configuration des droits d’accès aux imprimantes,
- la gestion centralisée des pilotes et filtres d’impression,
- la surveillance des travaux et des erreurs d’impression.

---

# 🧱 Concepts clés du serveur d’impression

### 📌 Files d’impression 
Chaque imprimante partagée possède une **file d’attente** dans laquelle sont stockés les travaux d’impression avant leur envoi.

Infos gérées par le serveur :
- statut de l’imprimante (en ligne / hors ligne),
- file d’attente,
- priorité des impressions,
- gestion des incidents (papier, toner…).

### 📌 Pilotes d’impression
Les pilotes installés sur le serveur sont automatiquement propagés aux clients.

Types :
- Pilotes **v4** (modernes, plus sécurisés),
- Pilotes **Type 3** (compatibilité),
- Pilotes spécifiques constructeur (HP, Canon, Ricoh…).

### 📌 Protocoles utilisés
- **SMB** → partage des imprimantes via \\SERVEUR\Imprimante  
- **IPP** (Internet Printing Protocol)  
- **WSD** (Web Services for Devices)

### 📌 Déploiement via GPO
Les imprimantes peuvent être déployées automatiquement selon :
- les utilisateurs,
- les groupes AD,
- les unités organisationnelles (OU),
- les ordinateurs.

---

# 🔐 Rôle du serveur d'impression dans un environnement AD

Dans une infrastructure Active Directory, un serveur d’impression permet :

- l’attribution automatique d’imprimantes aux utilisateurs selon leur service,  
- la gestion des droits (lecture, gestion, suppression de jobs),  
- la centralisation des pilotes,  
- la standardisation du parc d’imprimantes,  
- la réduction des problèmes liés aux installations locales d’imprimantes.

Print Server + AD =  
➡️ déploiement propre et automatisé  
➡️ administration facilitée  
➡️ sécurité renforcée

---

## 🩺 Pourquoi un serveur d’impression est indispensable ?
- Centralisation des imprimantes au même endroit.  
- Gestion simplifiée pour les administrateurs.  
- Déploiement automatique sur les postes utilisateurs.  
- Contrôle des droits d’utilisation et des files.  
- Mises à jour de pilotes centralisées.
  
---

# 📑 Ce que j’ai déjà réalisé (Portfolio)

### 🔧 Travaux effectués sur serveur d’impression Windows Server

- Installation du rôle **Print and Document Services**.  
- Ajout et configuration d’imprimantes réseau (ports TCP/IP).  
- Partage d’imprimantes via SMB avec gestion des permissions.  
- Déploiement automatique d’imprimantes via **GPO**.  
- Tests d’impression avec utilisateurs et groupes Active Directory.  
- Gestion des files : suppression, priorités, incidents.  
- Vérification des droits via les ACL (Print, Manage Printers…).  
- Documentation du parc d’imprimantes et des pilotes utilisés.  

---

# 🛠️ Bonnes pratiques pour un serveur d’impression

**Déployer les imprimantes via GPO**
Pas manuellement.  

**Créer une imprimante par service**
Lorsqu'il y a un risque de surcharge.  

**Utiliser des ports TCP/IP fixes**
Pas WSD (trop instable).  

**Séparer les permissions** 
Entre utilisateurs et administrateurs. 

**Activer l’audit d'impression**
Si traçabilité requise.  

**Documenter les modèles et pilotes utilisés**
Pour homogénéiser le parc.  

**Superviser les files d'impression**
Pour détecter blocages et pannes récurrentes.
