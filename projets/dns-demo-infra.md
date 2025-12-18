---
title: DNS Mixte Windows + BIND
parent: Projets
nav_order: 4
---

# DNS Mixte : Zone primaire `demo.infra` sur BIND, répliquée sur Windows DNS

Ce chapitre présente la mise en place d’une zone DNS indépendante de l’Active Directory : **demo.infra**, hébergée en primaire sur un serveur **BIND Debian**, puis **répliquée sur SRV-FILE01** via transfert de zone AXFR.  
Un **redirecteur conditionnel** est également configuré sur **SRV-AD01** pour déléguer la résolution à BIND.

Ce déploiement permet d'étudier un environnement **DNS mixte** (Linux / Windows) tout en gardant le domaine AD séparé (`Homelab.local`).

---

## 🎯 Objectifs

- Créer une zone DNS dédiée : **`demo.infra`** sur BIND  
- Répliquer la zone vers **SRV-FILE01 (Windows DNS secondaire)**  
- Mettre en place un **redirecteur conditionnel sur SRV-AD01** pour `demo.infra`  
- Tester la résolution depuis les environnements Linux et Windows  
- Démontrer la maîtrise d’une **infrastructure DNS multi-OS**  
- Gestion centralisée : **toutes les modifications se font sur BIND**

---

## 🖥️ Architecture DNS

| Serveur       | Rôle                           | OS         | IP          |
|---------------|---------------------------------|------------|-------------|
| **SRV-DNS01** | DNS primaire – BIND (master)    | Debian 12  | 10.30.0.10  |
| **SRV-FILE01**| DNS secondaire – Transfert AXFR | Win 2022   | 10.50.0.10  |
| **SRV-AD01**  | Redirecteur conditionnel        | Win 2022   | 10.20.0.10  |

**Diagramme logique DNS :**  
![Diagramme DNS demo.infra](images/dns-demo-infra.png)

---

## 🗂️ Structure de la zone `demo.infra`



La zone est **entièrement gérée sur BIND**, puis reproduite telle quelle sur Windows via AXFR.

---

## 🔧 Mise en œuvre

### 🔹 Déploiement du serveur BIND (primaire)

- Création de la VM **SRV-DNS01**
- Installation de **Debian 12**  
- Installation du paquet : `bind9`  
- Création de la zone **primaire** :  
- Création du fichier de zone  
- Vérification de la configuration (`named-checkconf` / `named-checkzone`)

![Zone Bind](/admin.homelab/assets/images/zone-bind.png)

---

### 🔹 Mise en place du DNS secondaire sur SRV-FILE01

- Installation du role **DNS** 
- Ajout d’une nouvelle zone **secondaire** dans Windows DNS  
- Adresse du maître : **10.30.0.10 (BIND)**  
- Validation du transfert de zone AXFR  
- Vérification de la réplication automatique

![Windows DNS secondaire](/admin.homelab/assets/images/windows-dns.png)

---

### 🔹 Redirecteur conditionnel sur SRV-AD01

Sur le serveur AD01, création d’un redirecteur conditionnel :

Zone : demo.infra
Cible : 10.30.0.10 (SRV-DNS01)

Résultat :  
➡️ Tout ce qui concerne `demo.infra` est envoyé **exclusivement** vers BIND.

![Redirecteur conditionnel](/admin.homelab/assets/images/windows-dns-redirecteur.png)
---

### 🔹 Validation & supervision

- Tests avec **nslookup**, **dig**, **Resolve-DnsName**  
- Fonctionnement constaté :
  - Les serveurs AD délèguent la résolution via redirecteur  
  - BIND reste la **source d’autorité**  

![Test nslookup](/admin.homelab/assets/images/dns-nslookup.png)

---

## 📄 Documentation complémentaire

[DNS Mixte – PDF](/admin.homelab/assets/pdfs/dns-mixte.pdf)

---