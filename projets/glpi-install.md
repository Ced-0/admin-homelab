---
title: GLPI Installation
parent: Projets
nav_order: 8
---

# Installation et Configuration de GLPI

Cette page décrit le déploiement de **GLPI** (Gestionnaire Libre de Parc Informatique) pour la gestion des tickets, des actifs et du support utilisateur. L’objectif est d’avoir un outil centralisé pour le helpdesk et le suivi des incidents.

---

## 🎯 Objectifs

- Installer GLPI sur le serveur **SRV-GLPI01**  
- Configurer la base de données et l’accès web sécurisé (HTTPS)  
- Intégrer GLPI avec **Active Directory** pour l’authentification des utilisateurs  
- Installer et configurer les agents GLPI sur les postes clients  
- Préparer les plugins nécessaires pour inventaire matériel et logiciel  

---

## 🖥️ Architecture GLPI

| Composant       | Rôle                  | IP         |
|-----------------|---------------------|-----------|
| SRV-GLPI01      | Serveur GLPI         | 10.50.0.30 |
| Postes Clients  | Accès GLPI          | VLAN 40 (Clients) |

**Diagramme logique GLPI :**  
![Diagramme GLPI](/admin.homelab/assets/images/glpi-architecture.png)

---

## 🔧 Mise en œuvre

### 🔹 Installation et configuration du serveur GLPI
- Création de la VM **SRV-GLPI01**
- Installation de **Debian 12**  
- Installation de GLPI  
- Configuration du serveur web **Apache** et la base de données **MariaDB**  
- Activer **HTTPS** pour sécuriser l’accès web (certificat signé par SRV-PKI01)   

![Installation GLPI](/admin-homelab/assets/images/glpi-installation.png)

---

### 🔹 Intégration Active Directory
- Configurer l’**authentification LDAP** vers le domaine `Homelab.local` 
- Configurer l'attribution automatique du profil GLPI (Self-service, Technicien..)   
- Vérifier la **connexion des utilisateurs AD** à GLPI  
 

![Intégration AD GLPI](/admin-homelab/assets/images/glpi-ad-integration.png)

---

### 🔹 Fonctionnalités supplémentaires
- Possibilité d’installer des **agents GLPI** sur les postes clients pour l’inventaire automatique  
- Possibilité de configurer des **notifications et automatisation de tickets** via plugins  
- Ces fonctionnalités sont optionnelles et ne seront pas exploitées dans ce lab

---

### 🔹 Vérification et tests
- Vérifier que tous les utilisateurs AD peuvent **se connecter selon leurs droits**  
- Créer un **ticket test** pour valider la réception par le helpdesk  
- Contrôler la sécurisation **HTTPS** et les droits d’accès  

![Vérification GLPI](/admin-homelab/assets/images/glpi-verification.png)

---

### 📄 Documentation complémentaire
- PDF final du déploiement : [GLPI Installation](/admin-homelab/assets/pdfs/glpi-installation.pdf)