---
title: DHCP Mixte Windows + ISC
parent: Projets
nav_order: 5
---

# DHCP Mixte : Windows + ISC (Debian)

Cette page détaille la mise en place d’un **DHCP mixte**, combinant :  
- **DHCP Windows Server** pour la majorité des postes  
- **ISC DHCP sur Debian** pour VLAN spécifiques ou redondance limitée  

⚠️ **Important** : il n’y a **pas de failover complet** entre Windows et ISC Debian. Seul un mode “split-scope” peut être mis en place, aucune tolérance aux pannes réelle.

---

## 🎯 Objectifs

- Déployer un scope DHCP principal sur Windows pour les postes clients  
- Installer ISC DHCP sur Debian comme serveur secondaire / split-scope pour VLAN spécifiques  
- Mettre en place des réservations pour les serveurs critiques (AD, File, Print, Exchange, GLPI)  
- Assurer cohérence et attribution correcte des IP  
- **Remarque** : Windows ↔ Debian = split-scope uniquement, pas de failover complet

---

## 🖥️ Architecture DHCP

| Serveur    | Rôle                   | OS        | IP             |
|-----------|----------------------|-----------|----------------|
| SRV-DHCP01 | DHCP principal Windows | Win 2022  | 10.30.0.20 |
| SRV-DHCP02 | DHCP secondaire ISC   | Debian 12 | 10.30.0.21 |

**Diagramme logique DHCP :**  
![Diagramme DHCP](/admin.homelab/assets/images/dhcp-architecture.png)

---

## 🔧 Mise en œuvre DHCP

### 🔹 Déploiement du serveur DHCP Windows
- Installation et configuration de **Windows Server 2022** sur SRV-DHCP01  
- Création du **scope principal pour VLAN 40** (Postes clients)  
- Définition des **réservations pour serveurs critiques** : AD, File, Print, Exchange, GLPI  
- Configuration des **options DHCP** : DNS, Gateway, NTP  
- Test de l’attribution d’IP sur des postes clients Windows et Linux  

**Screenshot DHCP Windows :**  
![DHCP Windows](/admin.homelab/assets/images/dhcp-windows.png)

---

### 🔹 Déploiement du serveur ISC DHCP Debian
- Installation du package `isc-dhcp-server` sur SRV-DHCP02  
- Définition des **subnets spécifiques** pour VLAN ou split-scope  
- Ajout des **réservations pour serveurs critiques**  
- Test de l’attribution d’IP avec `dhclient` sur un poste Debian  
- Vérification que le **split-scope fonctionne correctement**, en lecture seule pour les IP non critiques  

**Screenshot ISC DHCP :**  
![DHCP ISC](/admin.homelab/assets/images/dhcp-isc.png)

---

### 🔹 Vérification et tests
- Tous les postes clients reçoivent une **IP correcte selon le VLAN et le scope**  
- Les **réservations serveur** sont bien appliquées  
- Le **split-scope Windows ↔ Debian** fonctionne, mais **aucune tolérance aux pannes complète** n’est mise en place  
- Captures ou logs disponibles pour **documentation et suivi**

---

**Placeholder PDF ou capture finale DHCP :**  
[DHCP Documentation PDF](/admin.homelab/assets/pdfs/dhcp-mixte.pdf)

