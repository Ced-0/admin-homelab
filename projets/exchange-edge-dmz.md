---
title: Exchange Edge en DMZ
parent: Projets
nav_order: 11
---

# 💼 Déploiement Exchange Edge en DMZ

Déploiement d’un **serveur Exchange Edge Transport** pour sécuriser les flux SMTP entre l’environnement interne Exchange et l’extérieur.  
Le rôle Edge est isolé dans une **DMZ**, ne rejoint pas le domaine Active Directory et renforce la protection de la messagerie grâce au filtrage SMTP et aux mécanismes anti-spam.

---

## 🎯 Objectifs

- Déployer un serveur **Exchange Edge Transport** sur **SRV-EXCH-EDGE**  
- Isoler le serveur dans la **DMZ** pour renforcer la sécurité  
- Configurer le **routage SMTP** entre Internet et Exchange interne  
- Mettre en place les protections **anti-spam** et filtres SMTP  
- Synchroniser la configuration via une **Edge Subscription**  

---

## 🖥️ Architecture Exchange Edge

| Serveur         | Rôle              | IP / VLAN        |
|-----------------|-------------------|------------------|
| SRV-EXCH-EDGE   | Edge Transport    | 10.70.0.30 (DMZ) |
| SRV-EXCH01      | Mailbox interne   | 10.50.0.40       |
| SRV-AD01        | Active Directory  | 10.20.0.10       |

**Caractéristiques principales :**  
- Serveur **non joint au domaine**  
- Routage SMTP sécurisé via **EdgeSync**  
- Isolation complète en DMZ  

**Diagramme logique Exchange Edge :**  
![Diagramme logique Exchange Edge](/admin.homelab/assets/images/exchange-edge-diagram.png)

---

## 🔧 Mise en œuvre

### 🔹 Préparation du serveur
- Mise en place du serveur **Windows Server 2022** dédié au rôle Edge, configuré sur le VLAN DMZ et isolé du domaine conformément aux bonnes pratiques Exchange.  
- Configuration réseau, durcissement de l’hôte et ouverture des flux strictement nécessaires.

![Préparation serveur Edge](/admin.homelab/assets/images/exchange-edge-prep.png)

### 🔹 Déploiement du rôle Edge Transport
- Installation du rôle **Exchange Edge Transport**, application des mises à jour et validation des services de transport.  
- Activation des modules anti-spam intégrés au rôle.

![Installation Edge Transport](/admin.homelab/assets/images/exchange-edge-install.png)

### 🔹 Mise en place du routage et de la synchronisation
- Création et importation de la **Edge Subscription** permettant la synchronisation sécurisée avec Exchange interne.  
- Mise en place des connecteurs SMTP pour l’acheminement entrant/sortant et configuration du chiffrement **TLS SMTP**.

![Edge Subscription et Routage](/admin.homelab/assets/images/exchange-edge-subscription.png)

### 🔹 Renforcement de la sécurité
- Application des restrictions firewall, isolation totale en DMZ. 
- Validation des mécanismes de filtrage et du comportement anti-spam.

![Sécurisation Edge Transport](/admin.homelab/assets/images/exchange-edge-security.png)

---

## ✔️ Résultats

- Serveur **Edge Transport pleinement opérationnel** en zone DMZ  
- Acheminement SMTP entrant et sortant fonctionnel  
- Synchronisation EdgeSync active et fiable  
- Protection anti-spam et filtrage SMTP opérationnels  
- Architecture Exchange renforcée et conforme aux bonnes pratiques de sécurité  

---

## 🧠 Compétences mises en avant

- Déploiement **Microsoft Exchange Edge Transport**  
- Routage **SMTP sécurisé** et connecteurs de transport  
- Gestion de **EdgeSync**  
- Sécurisation réseau en **DMZ**  
- Mise en place de mécanismes anti-spam Exchange  
- Architecture messagerie segmentée DMZ / LAN  

---

## 📎 Ressources associées

[exchange-edge-deployment.pdf](/admin.homelab/assets/pdfs/exchange-edge-deployment.pdf)

