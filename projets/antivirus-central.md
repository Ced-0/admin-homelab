---
title: Antivirus & Supervision Wazuh
parent: Projets
nav_order: 9
---

# Wazuh – Antivirus & Supervision

Cette page présente le déploiement d’un serveur **Wazuh** pour la supervision et la gestion des événements de sécurité dans le lab, avec des agents Windows et linux pour le suivi antivirus et les logs système.

---

## 🎯 Objectifs

- Déployer un serveur **Wazuh Manager** centralisé  
- Installer les **agents Wazuh** sur postes et serveurs Windows_Debian  
- Vérifier la remontée des logs antivirus et événements système  
- Visualiser les événements dans le **dashboard Wazuh**  

---

## 🖥️ Architecture Wazuh

| Composant       | Rôle                         | OS        | VLAN / IP        |
|-----------------|------------------------------|-----------|-----------------|
| SRV-WAZUH01     | Wazuh Manager + Dashboard    | Linux     | VLAN Infra / 10.30.0.50 |
| Postes Clients  | Agents Wazuh                 | Windows   | VLAN Clients    |
| SRV-AD01        | Source de logs AD            | Windows   | VLAN Infra      |

**Diagramme simplifié Wazuh :**  
![Diagramme Wazuh](/admin.homelab/assets/images/wazuh-architecture.png)

---

## 🔧 Mise en œuvre

### 🔹 Installation du serveur Wazuh
- Déploiement de la VM **SRV-WAZUH01**  
- Installation de Wazuh Manager + Dashboard  
- Vérification de l’accès au dashboard  
- Activer **HTTPS** pour sécuriser l’accès web (certificat signé par SRV-PKI01)   

![Serveur Wazuh](/admin.homelab/assets/images/wazuh-dashboard.png)

---

### 🔹 Déploiement des agents Wazuh
- Création de **paquets WAPT** pour automatiser l’installation des agents
- Liaison des agents avec le **Wazuh Manager** via la clé d’enrôlement
- Vérification de la **remontée des logs** dans le dashboard

![Agents Wazuh](/admin.homelab/assets/images/wazuh-deploy.png)

---

### 🔹 Supervision simple
- Remontée des logs **Windows Defender** (antivirus)  
- Surveillance de quelques événements système  
- Visualisation des alertes dans le dashboard  

---

### 🔹 Vérification
- Vérification que tous les agents sont connectés au Manager  
- Contrôle que les événements sont bien visibles dans le dashboard  

---

## 📄 Documentation complémentaire

- PDF du déploiement simplifié : [wazuh-deployment.pdf](/admin.homelab/assets/pdfs/wazuh-deployment.pdf)

---
