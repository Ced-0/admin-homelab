---
title: PfSense Firewall
parent: Projets
nav_order: 2
---

# PfSense Firewall

Déploiement d’un **pare-feu PfSense** au sein du lab Hyper-V.  
Cette infrastructure a pour objectif de fournir un réseau **segmenté, sécurisé et extensible**, supportant tous les services du lab (AD, File, Exchange, RDS, VoIP…).

---

## 🎯 Objectifs du projet

- Installer PfSense comme **firewall principal** du lab  
- Définir une **topologie réseau logique** et des VLANs pour isoler les services  
- Assurer le **routage interne et l’accès Internet**  
- Préparer le lab pour l’intégration future des services : DMZ, VPN, supervision...

---

## 🖥️ Architecture réseau

- **WAN** : Internet simulé via Hyper-V NAT ou adaptateur externe  
- **LAN / VLANs** :

| VLAN | Gateway        | Description                                          |
|------|----------------|------------------------------------------------------|
| 10   | 10.10.0.1      | Management (IT, Rustdesk)                            |
| 20   | 10.20.0.1      | Domain Controllers                                   |
| 30   | 10.30.0.1      | Infrastructure (DNS, DHCP, PKI, WAPT, Wazuh)         |
| 40   | 10.40.0.1      | Clients                                              |
| 50   | 10.50.0.1      | Services utilisateurs (File, Print, GLPI, Exchange, RDS) |
| 60   | 10.60.0.1      | VoIP (Xivo)                                          |
| 70   | 10.70.0.1      | DMZ                                                  |
| 80   | 10.80.0.1      | Supervision (Zabbix)                                 |
| 90   | 10.90.0.1      | Backup (Bacula)                                      |
| 100  | 10.100.0.1     | Imprimantes réseaux                                  |

## 🔧 Mise en œuvre

### 🔹 Déploiement
- Création d’une VM dédiée (2 interfaces : WAN / LAN)
- Installation du système PfSense
- Attribution et vérification des interfaces

### 🔹 Segmentation réseau
- Création de l’ensemble des VLANs nécessaires
- Association des VLANs aux interfaces internes
- Organisation logique des sous-réseaux et plages IP

### 🔹 Règles de filtrage
- Mise en place d’une politique inter-VLAN restrictive
- Autorisation progressive des flux selon les besoins fonctionnels
- Configuration du NAT pour la sortie Internet

### 🔹 Intégration aux services du lab
- DHCP déporté sur les serveurs Windows / ISC
- Préparation pour l’intégration future : VPN, DMZ, supervision, sauvegardes…

## 📸 Interface & supervision
![PfSense Dashboard](/admin.homelab/assets/images/pfsense-dashboard.png)

## ✅ Vérification
- Vérifier que les VLANs sont correctement créés et accessibles selon le plan IP
- Tester la connectivité de base entre LAN et WAN
- Capturer les logs PfSense pour valider les interfaces et le routage

## 📄 Documentation complémentaire
[pfsense-configuration.pdf](/admin.homelab/assets/pdfs/pfsense-configuration.pdf)

---
