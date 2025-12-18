---
title: Déploiement RDS
parent: Projets
nav_order: 14
---

# 💼 Déploiement Remote Desktop Services (RDS)

Déploiement d’une infrastructure **Remote Desktop Services (RDS)** permettant un accès distant sécurisé aux bureaux et applications du lab.  
L’architecture repose sur une **séparation stricte des rôles**, une **segmentation réseau par VLAN**, et une **exposition sécurisée via un reverse proxy HAProxy**.

L’authentification est assurée par **Network Policy Server (NPS)** intégré à **RD Gateway**, avec une architecture **prête pour l’intégration de solutions MFA**.

---

## 🎯 Objectifs

- Déployer une infrastructure **RDS multi-rôles** conforme aux bonnes pratiques Microsoft
- Séparer les rôles **RD Gateway**, **RD Connection Broker** et **RD Session Host**
- Sécuriser l’accès distant via **RD Gateway exposé derrière HAProxy**
- Centraliser l’authentification via **NPS (RADIUS intégré)**
- Publier des bureaux et applications distantes aux utilisateurs Active Directory
- Appliquer des politiques de sécurité via **GPO**, **NLA** et **PKI interne**
- Concevoir une architecture **évolutive et compatible MFA**

---

## 🖥️ Architecture RDS

| Serveur       | Rôle                                   | IP                     |
|---------------|----------------------------------------|------------------------|
| RDS-Gateway   | RD Gateway + NPS (RADIUS intégré)      | 10.30.0.60             |
| RDS-Broker    | RD Connection Broker                   | 10.30.0.70             |
| SRV-RDS01     | RD Session Host                        | 10.50.0.50             |
| HAProxy       | Reverse Proxy HTTPS                    | VPS / Frontend         |
| Clients AD    | Postes utilisateurs                    | VLAN Utilisateurs      |

**Services déployés :**
- Remote Desktop Gateway  
- Remote Desktop Connection Broker  
- Remote Desktop Session Host  
- Network Policy Server (NPS)  
- Reverse proxy HAProxy  

**Accès utilisateur :**  
`https://rdp.nebulo.games/rdweb`

**Flux de connexion :**
1. Client → HAProxy (HTTPS)
2. HAProxy → RD Gateway
3. RD Gateway → RD Connection Broker
4. Broker → RD Session Host

**Diagramme logique RDS :**  
![Architecture RDS](/admin-homelab/assets/images/rds-architecture.png)

---

## 🗂️ Gouvernance Active Directory et séparation des rôles

### Organisation des OU

Chaque rôle RDS dispose de sa **propre unité d’organisation (OU)** afin de :
- cibler précisément les GPO
- éviter les effets de bord
- garantir la cohérence de configuration
- faciliter l’industrialisation

> 🧠 Principe clé  
> **1 rôle = 1 OU = 1 jeu de GPO**

### Arborescence AD mise en place  

```
OU=Serveurs
└─ OU=RDS
├─ OU=SessionHosts
│ ├─ SRV-RDS01
├─ OU=Gateway
│ └─ RDS-Gateway
└─ OU=Broker
└─ RDS-Broker
```

---

## 🔧 Mise en œuvre

### 🔹 Création des OU et préparation AD

- Création des **OU RDS dédiées**
- Déplacement des serveurs dans leur OU respective
- Désactivation de l’héritage des GPO génériques si nécessaire
- Préparation des **groupes AD** (accès RDS, administration)

![Préparation Active Directory RDS](/admin-homelab/assets/images/rds-ad-preparation.png)

---

### 🔹 Déploiement du RD Session Host

- Installation du rôle **Remote Desktop Session Host** sur **SRV-RDS01**
- Tous les paramètres du Session Host sont **exclusivement gérés par GPO**

![RD Session Host](/admin-homelab/assets/images/rds-session-host.png)

---

### 🔹 Gouvernance des Session Hosts par GPO

Les **RD Session Hosts sont considérés comme des serveurs jetables**.  
Toute la configuration est déclarative et centralisée.
  
- Limites de temps des sessions
- Déconnexion automatique
- Redirections de périphériques
- Expérience utilisateur (graphismes, audio)

Aucune modification manuelle n’est conservée sur les hosts.

![GPO Session Host](/admin-homelab/assets/images/rds-gpo-sessionhost.png)

---

### 🔹 Déploiement du RD Connection Broker

- Installation du rôle **RD Connection Broker** sur **RDS-Broker**
- Centralisation des connexions
- Gestion de **MA_collection RDS**
- Attribution dynamique des sessions aux Session Hosts

![RD Connection Broker](/admin-homelab/assets/images/rds-broker.png)

---

### 🔹 Déploiement du RD Gateway et NPS

- Installation du rôle **RD Gateway** sur **SRV-RDS-GW**
- Intégration Active Directory 
- Configuration des **CAP** et **RAP**
- Activation de **Network Policy Server (NPS)**
- Activation de la **Network Level Authentication (NLA)**

![RD Gateway](/admin-homelab/assets/images/rds-gateway.png)

---

### 🔹 Publication sécurisée via HAProxy

- Exposition des services RDS via **HAProxy**
- Fonctionnement en **reverse proxy HTTPS**
- Terminaison TLS via **PKI interne**
- Redirection sécurisée vers RD Gateway

![HAProxy Reverse Proxy RDS](/admin-homelab/assets/images/rds-haproxy.png)

---

## 🔐 Authentification et MFA

L’authentification repose sur **NPS intégré** à RD Gateway.  
L’architecture est compatible avec des solutions MFA telles que :

- **Microsoft Entra ID MFA** (extension NPS)
- **Duo Security for RD Gateway**
- **Serveur RADIUS dédié** (NPS ou solution tierce)

> ⚠️ Ces solutions MFA ne sont **pas implémentées dans ce projet**, mais l’architecture est **prête à les intégrer**.

---

## ✔️ Résultats

- Architecture **RDS segmentée et gouvernée**
- Séparation claire des rôles et des responsabilités
- **Session Hosts pilotés exclusivement par GPO**
- Accès distant sécurisé via RD Gateway et HAProxy
- Infrastructure évolutive et conforme aux bonnes pratiques

---

## 🧠 Compétences mises en avant

- Architecture **Remote Desktop Services**
- Gouvernance Active Directory par OU
- Centralisation de la configuration via **GPO**
- Sécurisation des accès distants
- Conception d’architectures **MFA-ready**
- Industrialisation et maintenabilité des environnements RDS

---

## 📎 Ressources associées

[rds-deployment.pdf](/admin-homelab/assets/pdfs/rds-deployment.pdf)