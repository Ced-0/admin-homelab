---
title: "Architecture VLAN"
parent: Projets
nav_order: 1
---

# Architecture VLAN

Cette page décrit la **segmentation logique du réseau** pour le lab Hyper-V. Chaque VLAN est défini par son rôle et les services associés, permettant d’isoler et sécuriser l’infrastructure.

---

## 🎯 Objectifs

- Définir les VLANs pour **séparer les services critiques**  
- Préparer l’architecture réseau pour PfSense et les serveurs du lab  
- Garantir isolation et QoS pour VoIP et flux sensibles  
- Fournir un schéma clair pour la documentation et la présentation au recruteur

---

## 🗂️ Découpage VLAN

| **VLAN**                         | **Composants**                                                                    | **Rôle**                                                                                                                           |
| -------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **VLAN 10 (Management)**         | PC IT (postes clients), SRV-MGMT01 (RustDesk)                                     | Gestion de l'infrastructure IT, accès à distance via RustDesk, gestion des définitions antivirus, mise à jour des agents antivirus |
| **VLAN 20 (Domain Controllers)** | SRV-AD01, SRV-AD02                                                                | Contrôleurs de domaine (Active Directory)                                                                                          |
| **VLAN 30 (Infra)**              | SRV-DNS01, SRV-DHCP01, SRV-PKI01, SRV-WAPT01                                      | Services d'infrastructure supplémentaires (DNS, DHCP, PKI)                                                                         |
| **VLAN 40 (Clients)**            | Postes clients (PC des utilisateurs)                                              | Postes de travail utilisateurs : Accès aux services partagés, domaine, etc.                                                        |
| **VLAN 50 (Services)**           | SRV-FILE01, SRV-PRINT01, SRV-GLPI01, SRV-EXCH01, SRV-RDS01, SRV-EDR01 (Wazuh)     | Services utilisateurs (fichiers, impression, GLPI, Exchange, RDS, gestion des antivirus pour les postes clients)                   |
| **VLAN 60 (Voice)**              | SRV-PBX01, Téléphones IP                                                         | Téléphonie IP (VoIP) : Serveur VoIP et périphériques associés (téléphones IP)                                                      |
| **VLAN 70 (DMZ)**                | RDS Gateway, SRV-EXCH-EDGE                                                        | Services exposés à Internet (RDS Gateway, Exchange Edge)                                                                           |
| **VLAN 80 (Supervision)**        | SRV-ZBX01                                                                         | Monitoring et supervision (Zabbix)                                                                                                 |
| **VLAN 90 (Backup)**             | SRV-Bacula (Serveur de sauvegarde), NAS-BACKUP01 (NAS)                            | Sauvegardes et stockage sécurisé des données                                                                                       |
| **VLAN 100 (Impression)**        | Imprimantes réseau                                                                | VLAN dédié aux imprimantes pour isoler et gérer les flux d'impression                                                              |

---

## 🌐 Diagramme logique VLAN

![Diagramme VLAN](images/vlan-diagram.png)

## 🔧 Notes de configuration

- Chaque VLAN est géré par PfSense en tant que **sous-interface VLAN** sur l’interface LAN
- Les flux seront **restreints par défaut** et ouverts uniquement selon le besoin
- VoIP (VLAN60) bénéficie d’une **priorité QoS** pour la téléphonie
- Backup et Storage sont isolés pour **sécuriser les données critiques**
- DMZ contient uniquement les serveurs exposés pour limiter la surface d’attaque

---

## ✅ Vérification

- Tester l’accès entre VLANs selon les règles définies
- Vérifier que le VLAN VoIP a **priorité QoS** sur le réseau
- Valider que les serveurs sensibles (AD, Backup, Storage) sont isolés

---
