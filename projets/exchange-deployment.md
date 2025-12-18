---
title: Exchange Server Interne
parent: Projets
nav_order: 10
---

# 💼 Déploiement Exchange Server Interne

Déploiement d’un **serveur Exchange Server 2019** pour la messagerie interne du lab.  
L’objectif est de fournir un service centralisé, intégré à **Active Directory**, sécurisé via la **PKI interne**, et préparé pour une future ouverture vers l’extérieur via une configuration standard reposant sur un **rôle Edge Transport** installé en DMZ.  
Les accès **OWA** et **Autodiscover** seront également publiés via un **reverse proxy**.

---

## 🎯 Objectifs

- Installer **Exchange 2019** sur le serveur interne **SRV-EXCH01**
- Intégrer Exchange au domaine et à l’annuaire Active Directory
- Créer les boîtes aux lettres internes pour les utilisateurs du lab
- Configurer les URL internes, la base de données et les politiques de boîtes
- Sécuriser les accès via certificat **PKI interne**

---

## 🖥️ Architecture Exchange

| Serveur       | Rôle                      | IP               |
|---------------|---------------------------|------------------|
| SRV-EXCH01    | Exchange interne (Mailbox)| 10.50.0.40       |
| SRV-AD01      | Active Directory / DNS    | 10.20.0.10       |
| Clients AD    | Outlook / OWA             | VLAN 40 (Clients)|

**Services principaux :**  
- OWA / ECP (HTTPS)  
- Autodiscover  
- MAPI over HTTP  
- SMTP interne  

**Accès interne :** `https://mail.nebulo.games/owa`

**Diagramme logique Exchange interne :**  
![Diagramme Exchange interne](/admin-homelab/assets/images/exchange-internal.png)

---

## 🔧 Mise en œuvre

### 🔹 Préparation du serveur
- Installation de Windows Server et intégration au domaine  
- Préparation AD et vérification DNS  
- Configuration du stockage destiné aux bases Exchange

![Préparation du serveur Exchange](/admin-homelab/assets/images/exchange-preparation.png)

### 🔹 Installation Exchange
- Déploiement d’Exchange 2019 en rôle Mailbox  
- Mise en place de la base de données et du stockage dédié    
- Configuration des services internes (OWA, ECP, Autodiscover)  

![Exchange Installation](/admin-homelab/assets/images/exchange-installation.png)

### 🔹 Intégration PKI interne
- Délivrance d’un certificat SSL via la PKI interne  
- Application du certificat aux services IIS  
- Vérification de la reconnaissance par les postes clients

![Certificat PKI Exchange](/admin-homelab/assets/images/exchange-pki.png)

### 🔹 Gestion des boîtes aux lettres
- Création des boîtes pour les utilisateurs internes  
- Application des quotas et stratégies locales  
- Organisation des boîtes dans la base dédiée

![Gestion Boîtes Exchange](/admin-homelab/assets/images/exchange-mailboxes.png)

### 🔹 Préparation pour la DMZ
- Vérification du fonctionnement SMTP interne  
- Préparation aux flux nécessaires pour Exchange Edge  
- Préparation future à la publication OWA/ActiveSync via reverse proxy

---

## ✔️ Résultats

- Messagerie interne totalement **opérationnelle** et **sécurisée**.  
- Accès **OWA** fonctionnel et intégré aux postes du domaine.  
- **Autodiscover** pleinement opérationnel pour Outlook.  
- Architecture prête pour l’intégration d’un **Edge Transport** et une publication externe sécurisée.  
- Base Exchange **stable**, monitoring et supervision en place.

---

## 🧠 Compétences mises en avant

- Administration **Microsoft Exchange Server 2019**  
- Intégration **Active Directory / DNS**  
- Gestion d’une **PKI interne**  
- Sécurisation **IIS / HTTPS**  
- Architecture réseau interne & pré-DMZ  
- Gestion de services de **messagerie professionnels**  
- Déploiement de services critiques en environnement **Windows Server**

---

## 📎 Ressources associées

[exchange-deployment.pdf](/admin-homelab/assets/pdfs/exchange-deployment.pdf)