---
title: Centralisation Syslog
parent: Projets
nav_order: 16
---

# Centralisation Syslog

Cette page décrit la mise en place d’une infrastructure de **centralisation des logs** pour tous les serveurs du lab, incluant Windows, Linux et équipements réseau. L’objectif est de collecter, centraliser et analyser les journaux pour supervision et sécurité.

---

## 🎯 Objectifs

- Installer un serveur **Syslog centralisé** sur SRV-ZBX01  
- Collecter les logs des serveurs Windows (Event Logs) et Linux (/var/log)  
- Centraliser les logs réseau (PfSense, Switchs virtuels)  
- Intégrer les logs avec **Zabbix** pour supervision  
- Permettre l’archivage et la consultation sécurisée  

---

## 🖥️ Architecture Syslog

| Composant       | Rôle                     | VLAN / IP          |
|-----------------|-------------------------|------------------|
| SRV-ZBX01       | Syslog centralisé / Zabbix | VLAN 80 192.168.80.10 |
| SRV-AD01/AD02   | Contrôleurs de domaine  | VLAN 20          |
| SRV-GLPI01      | GLPI                     | VLAN 50          |
| SRV-FILE01      | File Server              | VLAN 50          |
| SRV-PRINT01     | Print Server             | VLAN 50          |
| SRV-XIVO01      | VoIP                     | VLAN 60          |
| PfSense         | Firewall / VLAN routing  | VLAN 10/70       |

**Diagramme logique Syslog :**  
![Diagramme Syslog](images/syslog-architecture.png)

---

## 🔧 Installation et configuration

### 1️⃣ Installation du serveur Syslog

- Installer Linux (Debian/Ubuntu) sur SRV-ZBX01  
- Installer le service **rsyslog** ou équivalent pour la collecte des logs  

### 2️⃣ Configuration des agents

- Windows : installer **NXLog ou Winlogbeat** pour centraliser Event Logs  
- Linux : configurer rsyslog pour envoyer `/var/log` vers le serveur central  
- Equipements réseau : configurer PfSense pour envoyer logs syslog  

### 3️⃣ Organisation et filtrage

- Créer des fichiers logs séparés par source ou par type  
- Appliquer les filtres pour ne collecter que les événements pertinents  
- Mettre en place une rotation et archivage pour éviter de saturer le disque  

### 4️⃣ Intégration avec Zabbix

- Configurer Zabbix pour lire les logs et générer des alertes  
- Définir des triggers pour événements critiques (échecs authentification, erreurs systèmes, alertes PfSense)  

---

## ✅ Vérification

- Vérifier que tous les serveurs envoient correctement leurs logs  
- Contrôler la création des fichiers logs centralisés  
- Tester l’intégration avec Zabbix et les alertes  
- Valider la sécurité des fichiers et l’archivage  

---

## 🖼️ Placeholder image / screenshot Syslog

![Syslog Dashboard](images/syslog-dashboard.png)

---

## 📄 Placeholder PDF ou capture finale Syslog

[syslog-deployment.pdf](pdfs/syslog-deployment.pdf)
