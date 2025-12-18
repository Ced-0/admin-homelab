---
title: Projets
nav_order: 7
has_children: true
---

# Homelab – Projet Administrateur Système Junior

Bienvenue sur la page d’index de mon projet Homelab.  
Ce projet constitue l’un des éléments principaux de mon portfolio d’Administrateur Système Junior.  
Il simule l’infrastructure complète d’une PME moderne, avec une attention particulière portée à la sécurité, la segmentation réseau, la supervision et la documentation.

---

## 📚 Sommaire

- [1. Contexte et objectifs](#1-contexte-et-objectifs)
- [2. Objectifs techniques](#2-objectifs-techniques)
- [3. Utilisateurs et groupes Active Directory](#3-utilisateurs-et-groupes-active-directory)
- [4. Plan de VLAN](#4-plan-de-vlan)
- [5. Arborescences Serveurs](#5-arborescences-serveurs)
- [6. Plan d’adressage IP](#6-plan-dadressage-ip)
- [7. Sécurité & bonnes pratiques](#7-sécurité--bonnes-pratiques)
- [8. Livrables du portfolio](#8-livrables-du-portfolio)  
- [9. Critères de validation](#10-critères-de-validation)

---

# 1. Contexte et objectifs

## 1.1 Contexte
Ce homelab a pour but de démontrer mes compétences pratiques en administration système, réseau et sécurité au travers d’une infrastructure fonctionnelle et entièrement documentée.

## 1.2 Objectif général
Mettre en place un environnement professionnel complet incluant :

- Active Directory
- Services Windows et Linux
- Infrastructure réseau segmentée
- Sécurité (firewall, DMZ, PKI)
- Monitoring et logs centralisés
- Déploiement logiciel
- Sauvegardes
- Virtualisation

---

# 2. Objectifs techniques

## 2.1 Systèmes
- Windows Server 2019/2022  
- Linux (Debian, Ubuntu)  
- Scripts PowerShell & Bash  

## 2.2 Services Windows
- ADDS  
- DNS / DHCP  
- GPO  
- File & Print Server  
- RDS  
- Exchange / MTA  

## 2.3 Services Linux
- GLPI + FusionInventory  
- FusionPBX (VoIP)  
- Zabbix  
- Syslog centralisé
- WAPT
- Rustdesk
- Bacula  

## 2.4 Réseau & sécurité
- PfSense (VLAN, NAT, firewalls, DMZ, reverse proxy)
- VLAN 802.1Q
- QoS VoIP

## 2.5 Sauvegardes
- Bacula

---

# 3. Utilisateurs et groupes Active Directory

| Service              | Membres                                                |
|----------------------|--------------------------------------------------------|
| Direction            | Christian Hef, Pauline Atron, Pascaline Résident       |
| Comptabilité         | Bruno Ilan, Christelle Rédit, Florence Acture          |
| Secrétariat          | Cédric Ourrier, Sandrine Tandard, Aline Genda          |
| Production           | Chloé Hâne, Ursule Sine, Denis Elais                   |
| Support Informatique | Clément Lavier, Cédric Ambos, Elodie Cran              |

## Structure AD
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

# 4. Plan de VLAN

Utilisation d’un schéma d’adressage basé sur :  
**10.<VLAN>.0.0/24**

```
| VLAN | Nom | Rôle |
|------|------|------|
| 10 | Management | Administration |
| 20 | Domain Controllers | Active Directory |
| 30 | Infrastructure | Services critiques |
| 40 | Clients | Postes utilisateurs |
| 50 | Services | File/Print/GLPI/Exchange/RDS |
| 60 | VoIP | Téléphonie |
| 70 | DMZ | Services exposés |
| 80 | Monitoring | Supervision |
| 90 | Backup | Sauvegardes |
| 100 | Impression | Imprimantes |
```

---

# 5. Arborescences Serveurs

## 5.1 File Server – SRV-FILE01

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

- Méthode des permissions : **AGDLP**

---

# 6. Plan d’adressage IP

Format : **10.<VLAN>.0.x**

| Serveur | VLAN | Adresse |
|---------|------|----------|
| SRV-MGMT01 | 10 | 10.10.0.10 |
| SRV-AD01 | 20 | 10.20.0.10 |
| SRV-AD02 | 20 | 10.20.0.11 |
| SRV-DNS01 | 30 | 10.30.0.10 |
| SRV-DHCP01 | 30 | 10.30.0.20 |
| SRV-DHCP02 | 30 | 10.30.0.21 |
| SRV-PKI01 | 30 | 10.30.0.30 |
| SRV-WAPT01 | 30 | 10.30.0.40 |
| SRV-WAZUH01 | 30 | 10.30.0.50 |
| RDS-Gateway | 30 | 10.30.0.60 |
| RDS-Broker | 30 | 10.30.0.70 |
| SRV-FILE01 | 50 | 10.50.0.10 |
| SRV-PRINT01 | 50 | 10.50.0.20 |
| SRV-GLPI01 | 50 | 10.50.0.30 |
| SRV-EXCH01 | 50 | 10.50.0.40 |
| SRV-RDS01 | 50 | 10.50.0.50 |
| SRV-PBX01 | 60 | 10.60.0.10 |
| SRV-EXCH-EDGE | 70 | 10.70.0.10 |
| SRV-ZBX01 | 80 | 10.80.0.10 |
| SRV-BACKUP01 | 90 | 10.90.0.10 |
| NAS Backup | 90 | 10.90.0.20 |

---

# 7. Sécurité & bonnes pratiques

- Segmentation VLAN stricte  
- Firewall PfSense avec filtrage inter-VLAN  
- Reverse Proxy obligatoire en DMZ  
- ACL NTFS via AGDLP  
- Sauvegardes quotidiennes  
- Supervision de tous les services critiques  
- Export régulier des configurations (PfSense, GLPI, AD)

---

# 8. Livrables du portfolio

## Documentation
- Schéma réseau
- Schéma AD
- Plan d’adressage
- Table VLAN
- Règles PfSense
- Documentation GPO

## Scripts
- PowerShell (AD, partages, GPO)
- Bash (backups, supervision)
- WAPT (déploiements)

## Captures d’écran
- Installations
- Configurations
- Supervision
- GLPI / tickets
- DMZ / Reverse Proxy

## Procédures
- Ajout au domaine
- Onboarding utilisateur
- Restauration fichier
- Ouverture de flux firewall
- Gestion tickets GLPI

---

# 9. Critères de validation

- Infrastructure fonctionnelle et stable  
- VLAN isolés et sécurisés  
- Sauvegardes testées et restaurables  
- Documentation complète et professionnelle  
- Supervision opérationnelle

