---
title: FreePBX VoIP
parent: Projets
nav_order: 15
---

# Déploiement Xivo VoIP

Cette page décrit le déploiement d’un serveur **Xivo VoIP** dans le lab. L’objectif est de créer une infrastructure de téléphonie IP fonctionnelle, intégrée à l’Active Directory, avec des postes IP et un VLAN dédié pour la voix.

---

## 🎯 Objectifs

- Installer le serveur **Xivo** sur le serveur SRV-XIVO01  
- Configurer un VLAN dédié pour la voix (VLAN 60)  
- Déployer et enregistrer les téléphones IP  
- Intégrer Xivo avec **Active Directory** pour l’authentification des utilisateurs  
- Configurer les règles de QoS pour garantir la qualité des appels  
- Préparer la supervision via Syslog/Zabbix  

---

## 🖥️ Architecture Xivo

| Composant       | Rôle                     | VLAN / IP          |
|-----------------|-------------------------|------------------|
| SRV-XIVO01      | Serveur VoIP (Asterisk) | VLAN 60 192.168.60.10 |
| Téléphones IP   | Postes utilisateurs      | VLAN 60          |
| SRV-AD01        | Active Directory         | VLAN 20 192.168.20.10 |

**Diagramme logique Xivo :**  
![Diagramme Xivo VoIP](/admin-homelab/images/xivo-voip.png)

---

## 🔧 Installation et configuration

### 1️⃣ Préparation du serveur

- Installer Xivo sur Debian ou appliance virtuelle  
- Configurer l’IP statique sur VLAN 60  
- Mettre à jour le serveur et installer les dépendances  

### 2️⃣ Configuration de base

- Configurer Asterisk et le serveur VoIP  
- Créer les **extensions utilisateurs** et associer les téléphones IP  
- Appliquer les règles de routage et la gestion des appels internes  

### 3️⃣ Intégration Active Directory

- Synchroniser Xivo avec AD pour importer les utilisateurs  
- Appliquer les droits d’accès selon les groupes AD (Finance, HR, IT-Team)  

### 4️⃣ QoS et sécurité

- Activer la QoS sur le VLAN VoIP pour prioriser les appels  
- Configurer les règles firewall PfSense pour isoler la voix  
- Activer la journalisation via Syslog pour supervision  

### 5️⃣ Tests et validation

- Passer des appels internes entre postes  
- Tester l’appel vers l’extérieur (si simulé)  
- Vérifier la qualité audio et les logs  

---

## ✅ Vérification

- Tous les utilisateurs ont une extension fonctionnelle  
- Les appels internes fonctionnent correctement  
- QoS appliquée et isolation du VLAN vérifiée  
- Logs correctement centralisés vers Syslog/Zabbix  

---

## 🖼️ Placeholder image / screenshot Xivo

![Xivo Dashboard](/admin-homelab/images/xivo-dashboard.png)

---

## 📄 Placeholder PDF ou capture finale Xivo

[xivo-deployment.pdf](/admin-homelab/pdfs/xivo-deployment.pdf)
