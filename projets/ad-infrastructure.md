---
title: AD Deployment
parent: Projets
nav_order: 3
---

# Active Directory et Infrastructure

Ce chapitre présente le déploiement complet de l’infrastructure Active Directory dans un environnement Hyper-V local, incluant **ADDS**, **File Server**, **Print Server**, et **GPO/Hardening**. L’objectif est de créer une base stable et professionnelle pour tous les services du lab.

---

## 🎯 Objectifs

- Déployer un **domaine Active Directory** : `Homelab.local`  
- Installer deux contrôleurs de domaine : **SRV-AD01** (principal) et **SRV-AD02** (secondaire)  
- Déployer **File Server et Print Server** sur des machines distinctes  
- Créer les **OU**, groupes, utilisateurs et appliquer les **GPO de base**  
- Préparer la base pour Exchange, GLPI, RDS, WAPT et autres services  

---

## 🖥️ Architecture des serveurs

| Serveur       | Rôle               | OS        | IP         |
|---------------|--------------------|-----------|------------|
| SRV-AD01      | DC principal       | Win 2022  | 10.20.0.10 |
| SRV-AD02      | DC secondaire      | Win 2022  | 10.20.0.11 |
| SRV-FILE01    | File Server        | Win 2022  | 10.50.0.10 |
| SRV-PRINT01   | Print Server       | Win 2022  | 10.50.0.20 |

**Diagramme réseau / architecture AD :**  
![Diagramme réseau AD](/admin-homelab/assets/images/ad-network-diagram.png)

---

## 🗂️ Organisation des OU

```
Mon entreprise
│
├── Groupes
│   ├── Partages      ← Groupes locaux (droits sur les ressources)
│   └── Services      ← Groupes globaux (regroupent les utilisateurs)
│
├── Ordinateurs
│   ├── Clients       ← Postes utilisateurs
│   └── Serveurs      ← Machines serveurs
│
└── Utilisateurs      ← Comptes utilisateurs du domaine
```

---

## 👥 Groupes et utilisateurs

| Service              | Membres                                                |
|----------------------|--------------------------------------------------------|
| Direction            | Christian Hef, Pauline Atron, Pascaline Résident       |
| Comptabilité         | Bruno Ilan, Christelle Rédit, Florence Acture          |
| Secrétariat          | Cédric Ourrier, Sandrine Tandard, Aline Genda          |
| Production           | Chloé Hâne, Ursule Sine, Denis Elais                   |
| Support Informatique | Clément Lavier, Cédric Ambos, Elodie Cran              |


---

## 📂 File Server

1. Arborescence des partages :

- Serveur : **SRV-FILE01** 

```
F:
└── DATA  *(Accès Lecture pour tout le monde)*
    │
    ├── Services  *(Accès Lecture pour tout le monde)*
    │   ├── direction  *(Accès Modification pour la direction et comptabilité - Lecture pour les secrétaires)*
    │   ├── comptabilité  *(Accès Modification pour les comptables - Lecture pour la direction et les secrétaires)*
    │   ├── secrétariat  *(Accès Modification pour tous les secrétaires)*
    │   └── support  *(Accès Modification pour le support et les secrétaires - Lecture pour la direction)*
    │
    ├── Public  *(Accès Modification pour tout le monde)*
    │
    └── Informatique  *(dossier et partage caché — Accès Modification pour le service informatique)*
        └── gpo_ressources  *(Accès Lecture pour Domain Users, Modification pour le service informatique)*
    │
    └── Utilisateurs  *(Accès Modification pour chaque utilisateur sur son propre sous-dossier)*
        ├── User1  *(Accès Modification pour User1 uniquement)*
        ├── User2  *(Accès Modification pour User2 uniquement)*
        └── User3  *(Accès Modification pour User3 uniquement)*
```

2. ACL appliquées selon groupes AD
 
- Méthode AGDLP

| Dossier partagé   | Groupe DL à créer                                      |
|-------------------|--------------------------------------------------------|
| DATA              | `DL_DATA_RO`                                           |
| SERVICES          | `DL_SERVICES_RO`                                       |
| DIRECTION         | `DL_DIRECTION_RO`, `DL_DIRECTION_RW`                   |
| COMPTABILITE      | `DL_COMPTABILITE_RO`, `DL_COMPTABILITE_RW`             |
| SECRETARIAT       | `DL_SECRETARIAT_RW`                                    |
| SUPPORT           | `DL_SUPPORT_RO`, `DL_SUPPORT_RW`                       |
| PUBLIC            | `DL_PUBLIC_RW`                                         |
| INFORMATIQUE      | `DL_INFORMATIQUE_RW`                                   |
| GPO_RESSOURCES    | `DL_GPO_RESSOURCES_R0`, `DL_GPO_RESSOURCES_RW`         |
| UTILISATEURS      | *(pas de DL global — droits individuels)*              |

---

## 🔧 Mise en œuvre

### 🔹 Déploiement des serveurs
- Création des VM dédiées : **SRV-AD01, SRV-AD02, SRV-FILE01, SRV-PRINT01**  
- Installation de Windows Server 2022 sur chaque VM  
- Attribution des adresses IP selon le plan réseau (VLAN 20 pour les DC, VLAN 50 pour les serveurs de services)  
- Vérification de la connectivité avec le firewall PfSense  

![Déploiement des VM](/admin-homelab/assets/images/ad-vm-deployment.png)

---

### 🔹 Installation et configuration ADDS
- Promotion de **SRV-AD01** en Contrôleur de domaine principal (PDC)  
- Promotion de **SRV-AD02** en Contrôleur secondaire et vérification de la réplication  
- Configuration du **DNS interne** pour `Homelab.local`  
- Création des **Unités Organisationnelles (OU)** pour utilisateurs, groupes et ordinateurs  

![Configuration ADDS](/admin-homelab/assets/images/ad-setup.png)

---

### 🔹 Gestion des utilisateurs et groupes
- Création des **groupes de sécurité et distribution** selon la méthode AGDLP  
- Ajout des utilisateurs et assignation aux groupes  
- Vérification des droits d’accès sur les dossiers partagés  

![Gestion utilisateurs et groupes](/admin-homelab/assets/images/ad-users-groups.png)

---

### 🔹 File Server
- Installation du **File Server** sur SRV-FILE01  
- Création des **partages principaux** et application des ACL selon groupes AD  
- Test d’accès aux partages depuis un poste client  

![File Server](/admin-homelab/assets/images/ad-file-server.png)

---

### 🔹 Print Server
- Installation du **Print Server** sur SRV-PRINT01  
- Publication des imprimantes réseau par service ou département  
- Test d’accès aux imprimantes depuis les postes clients  

![Print Server](/admin-homelab/assets/images/ad-print-server.png)

---

### 🔹 GPO & Hardening
- Création et application des **GPO de sécurité** : complexité mot de passe, verrouillage
- Utilisation d'un fond d'écran d'entreprise  
- Déploiement des **partages et imprimantes** via GPO

![GPO & Hardening](/admin-homelab/assets/images/ad-gpo.png)

---

### 🔹 Vérification et supervision
- Vérification de la **réplication AD** entre SRV-AD01 et SRV-AD02  
- Test des **partages et imprimantes** selon les groupes  
- Contrôle de l’application des **GPO** sur les postes clients  
- Captures ou logs des services pour **documentation et suivi**  

---

## 📄 Documentation complémentaire

- PDF final du déploiement : [Domaine deploiement](/admin-homelab/assets/pdfs/ad-deployment.pdf)

---

