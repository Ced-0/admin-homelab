---
title: WAPT Deployment
parent: Projets
nav_order: 7
---

# Gestion Logicielle avec WAPT (Community)

Cette page décrit l'installation et la configuration de **WAPT Community**, solution de gestion logicielle pour les postes Windows du lab. Dans cette version gratuite, l’objectif est de **déployer et gérer les logiciels et mises à jour manuellement** sur les postes clients.  

> ⚠️ Le déploiement d’OS via PXE et les mises à jour automatiques sont **réservés à la version Enterprise** de WAPT.  
> Cette exploration permet néanmoins de se familiariser avec l’outil et ses concepts pour un usage futur plus avancé.

---

## 🎯 Objectifs

- Installer un serveur WAPT centralisé sur le lab avec **HTTPS sécurisé via PKI interne**  
- Déployer les agents WAPT sur les postes clients Windows via **GPO**  
- Créer et gérer des **packages logiciels** pour installation manuelle  
- Appliquer les mises à jour manuellement via les paquets WAPT  
- Découvrir la console d’administration WAPT et son fonctionnement  

---

## 🖥️ Architecture WAPT

| Composant | Rôle | IP / VM |
|-----------|------|---------|
| SRV-WAPT01 | Serveur WAPT (backend + serveur Apache/SQL, HTTPS PKI) | 10.30.0.40 |
| Postes clients | Agents WAPT installés via GPO | VLAN 40 (Clients) |

**Diagramme logique WAPT :**  
![Diagramme WAPT](/admin.homelab/assets/images/wapt-dashboard.png)

---

## 🔧 Mise en œuvre WAPT

### 🔹 Installation du serveur WAPT
- Installer et configurer le serveur WAPT **SRV-WAPT01** en standalone  
- Configurer le **SSL via certificat interne PKI** pour sécuriser les communications HTTPS  

![Installation serveur WAPT](/admin.homelab/assets/images/wapt-server-install.png)

---

### 🔹 Accès à la console WAPT Admin
- Se connecter à l’interface web sécurisée via HTTPS  
- Explorer les menus : packages, agents, tableaux de bord et rapports  
- Comprendre la gestion des paquets et la supervision centralisée  

![Console WAPT Admin](/admin.homelab/assets/images/wapt-console.png)

---

### 🔹 Déploiement des agents WAPT
- Installer l’agent sur les postes clients Windows via **GPO**   
- Vérifier que les agents communiquent correctement avec le serveur et peuvent recevoir des paquets  

![Installation agents WAPT](/admin.homelab/assets/images/wapt-agents.png)

---

### 🔹 Création et gestion de packages logiciels
- Créer des packages MSI   
- Déployer les packages manuellement   
- Tester le déploiement sur un poste pilote avant généralisation  

![Création packages WAPT](/admin.homelab/assets/images/wapt-packages.png)

> ⚠️ Les mises à jour Windows et logiciels doivent être gérées **manuellement** en créant des paquets correspondant aux KB ou versions à déployer.  
> Les fonctionnalités de mise à jour automatique et de déploiement d’OS sont réservées à WAPT Enterprise.

---

### 🔹 Vérification et suivi
- S’assurer que tous les agents sont correctement liés au serveur WAPT  
- Vérifier que les packages se déploient comme prévu  
- Consulter les rapports pour confirmer la réussite des installations et mises à jour manuelles  

![Monitoring WAPT](/admin.homelab/assets/images/wapt-monitoring.png)

---

### 🔹 Perspectives futures
- Explorer davantage WAPT pour automatiser la gestion des paquets  
- Tester l’intégration Enterprise pour le déploiement d’OS et la mise à jour automatique  
- Continuer à améliorer le lab et la supervision logicielle des postes Windows

---

### 🔹 Documentation complémentaire
[WAPT Documentation PDF](/admin.homelab/assets/pdfs/wapt-deployment.pdf)

---

