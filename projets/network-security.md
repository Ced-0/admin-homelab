---
title: Sécurité Réseau
parent: Projets
nav_order: 18
---

# Sécurité Réseau et Firewall

Cette page décrit la mise en place de la **sécurité réseau** dans le lab, incluant la configuration du firewall PfSense, la DMZ, l’isolation des VLANs et les règles d’accès. L’objectif est de protéger l’infrastructure tout en assurant la connectivité nécessaire aux services.

---

## 🎯 Objectifs

- Définir les règles de **firewall** pour tous les VLANs  
- Isoler les services sensibles (AD, Backup, Storage)  
- Configurer la **DMZ** pour exposer uniquement les services nécessaires (RDS Gateway, Exchange Edge, Reverse Proxy)  
- Appliquer le principe du **moindre privilège** sur tous les flux  
- Mettre en place la **sécurité des VLANs voix et management**  

---

## 🖥️ Architecture de sécurité

| VLAN / Segment        | Rôle / Protection                                  | Notes sécurité |
|----------------------|---------------------------------------------------|----------------|
| VLAN 20 - AD          | Contrôleurs de domaine                             | Accès restreint aux serveurs IT |
| VLAN 50 - Services    | File Server, Print Server, GLPI, Exchange, RDS    | Isolation inter-VLAN, accès uniquement via reverse proxy / RDS Gateway |
| VLAN 60 - VoIP        | Xivo et téléphones IP                              | QoS prioritaire, isolation stricte |
| VLAN 70 - DMZ         | RDS Gateway, Exchange Edge, Reverse Proxy         | Accès limité depuis Internet, règles NAT et firewall |
| VLAN 80 - Supervision | Zabbix / Syslog                                   | Accès limité, lecture seule pour monitoring |
| VLAN 90 - Backup      | SRV-VEEAM/BORG, NAS Backup                        | Isolé, uniquement pour serveurs autorisés |
| VLAN 10 - Management  | Postes IT et RustDesk                              | Sécurisé, accès contrôlé aux serveurs |

**Diagramme logique sécurité réseau :**  
![Diagramme sécurité réseau](images/network-security.png)

---

## 🔧 Configuration Firewall PfSense

### 1️⃣ Règles inter-VLAN

- Par défaut, **bloquer tous les flux** entre VLANs  
- Autoriser uniquement les flux nécessaires selon le rôle :  
  - VLAN 50 → VLAN 20 : accès aux DC pour authentification  
  - VLAN 50 → VLAN 90 : accès sauvegarde  
  - VLAN 60 → VLAN 50 : voix vers services internes  

### 2️⃣ NAT et DMZ

- Configurer **NAT** pour les services exposés en DMZ  
- Bloquer tout accès direct aux serveurs internes depuis Internet  
- Autoriser uniquement le reverse proxy, Exchange Edge, RDS Gateway  

### 3️⃣ QoS et priorisation

- VLAN 60 (VoIP) bénéficie d’une **priorité QoS**  
- VLAN Backup et Storage isolés pour sécuriser les flux critiques  

### 4️⃣ VPN / Accès externe

- Optionnel : configurer VPN pour accès sécurisé aux services internes  
- Restreindre VPN aux administrateurs IT  

---

## ✅ Vérification

- Tester les flux autorisés et bloqués entre VLANs  
- Vérifier l’accès aux services exposés via DMZ  
- Contrôler la QoS sur VLAN VoIP  
- Vérifier les logs PfSense pour détection d’accès non autorisés  

---

## 🖼️ Placeholder image / screenshot règles Firewall

![PfSense Rules](images/pfsense-rules.png)

---

## 📄 Placeholder PDF ou capture finale Firewall / DMZ

[network-security.pdf](pdfs/network-security.pdf)
