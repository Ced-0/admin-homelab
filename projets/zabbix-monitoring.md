---
title: Supervision Zabbix
parent: Projets
nav_order: 17
---

# Supervision Zabbix

Cette page décrit le déploiement de **Zabbix** pour la supervision complète de tous les services et serveurs du lab. L’objectif est de surveiller l’état des systèmes, des applications, des flux réseau et d’être alerté en cas de problèmes.

---

## 🎯 Objectifs

- Installer Zabbix Server sur **SRV-ZBX01**  
- Déployer les **agents Zabbix** sur tous les serveurs Windows et Linux  
- Collecter les métriques CPU, mémoire, disque, services, logs critiques  
- Superviser les équipements réseau (PfSense, VLAN, Xivo)  
- Configurer des alertes pour incidents et seuils critiques  
- Créer des dashboards pour visualiser l’état global du lab  

---

## 🖥️ Architecture Zabbix

| Composant       | Rôle                     | VLAN / IP          |
|-----------------|-------------------------|------------------|
| SRV-ZBX01       | Zabbix Server / DB       | VLAN 80 192.168.80.10 |
| SRV-AD01/AD02   | Agents Windows           | VLAN 20          |
| SRV-FILE01      | Agents Windows           | VLAN 50          |
| SRV-PRINT01     | Agents Windows           | VLAN 50          |
| SRV-GLPI01      | Agent Linux              | VLAN 50          |
| SRV-XIVO01      | Agent Linux              | VLAN 60          |
| PfSense         | SNMP / Monitoring        | VLAN 10/70       |

**Diagramme logique supervision Zabbix :**  
![Diagramme Zabbix](/admin-homelab/images/zabbix-architecture.png)

---

## 🔧 Installation et configuration

### 1️⃣ Installation du serveur Zabbix

- Installer Zabbix Server + Frontend + Base de données sur SRV-ZBX01  
- Configurer le firewall pour autoriser les agents à communiquer  

### 2️⃣ Déploiement des agents

- Windows : installer **Zabbix Agent** sur tous les serveurs  
- Linux : installer **Zabbix Agent** sur GLPI et Xivo  
- PfSense : configurer **SNMP** pour récupération des métriques  

### 3️⃣ Configuration des hôtes et templates

- Ajouter chaque serveur comme **host** dans Zabbix  
- Appliquer les templates standards pour OS, services, applications  
- Configurer des items personnalisés pour Exchange, RDS, GLPI, Xivo  

### 4️⃣ Alertes et dashboards

- Définir les triggers critiques (CPU > 80%, services arrêtés, disques pleins)  
- Configurer les notifications par email  
- Créer des dashboards synthétiques pour état global, réseau, services critiques  

### 5️⃣ Tests et validation

- Vérifier la remontée des métriques en temps réel  
- Simuler des incidents (arrêt service, surcharge CPU) et contrôler les alertes  
- Valider que toutes les machines et VLAN sont correctement supervisés  

---

## ✅ Vérification

- Tous les hôtes remontent correctement les métriques  
- Les alertes sont déclenchées en cas d’anomalie  
- Les dashboards reflètent l’état réel du lab  
- Les logs Zabbix sont cohérents et exploitables  

---

## 🖼️ Placeholder image / screenshot Zabbix

![Zabbix Dashboard](/admin-homelab/images/zabbix-dashboard.png)

---

## 📄 Placeholder PDF ou capture finale Zabbix

[zabbix-monitoring.pdf](/admin-homelab/pdfs/zabbix-monitoring.pdf)
