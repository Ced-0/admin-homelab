---
title: Reverse Proxy (Nginx)
parent: Projets
nav_order: 13
---

# 🌐 Publication des services Exchange 2019 via Nginx Reverse Proxy

Mise en place d’un **reverse proxy Nginx** dans la DMZ pour publier de manière sécurisée les services web Exchange vers Internet sous le domaine **mail.nebulo.games**.  
La solution permet une gestion centralisée du chiffrement, un contrôle complet des flux externes et une exposition maîtrisée des services OWA, ActiveSync, MAPI et Autodiscover.

---

## 🎯 Objectifs

- Publier les services Exchange 2019 via un **reverse proxy Nginx**  
- Exposer les services externes sur le domaine : **mail.nebulo.games**  
- Centraliser la gestion TLS et les certificats en frontal  
- Protéger Exchange interne en déportant l’exposition publique en DMZ  
- Garantir une publication conforme aux bonnes pratiques Microsoft  

---

## 🖥️ Architecture de publication

| Composant            | Rôle                              | IP / VLAN          |
|----------------------|-----------------------------------|--------------------|
| RP-NGINX01           | Nginx Reverse Proxy (DMZ)         | 10.70.0.20         |
| SRV-EXCH01           | Mailbox Exchange interne          | 10.50.0.40         |
| SRV-AD01             | Active Directory / DNS            | 10.20.0.10         |

**Services publiés :**  
- `https://mail.nebulo.games/owa`  
- `https://mail.nebulo.games/ecp`  
- `https://mail.nebulo.games/autodiscover`  
- `https://mail.nebulo.games/mapi`  
- `https://mail.nebulo.games/ews`  
- `https://mail.nebulo.games/Microsoft-Server-ActiveSync`

**Diagramme logique :**  
![Reverse Proxy Exchange](/admin.homelab/assets/images/exchange-reverseproxy.png)

---

## 🔧 Mise en œuvre

### 🔹 Déploiement du reverse proxy Nginx
Installation d’un serveur Nginx dédié dans la DMZ pour traiter l’ensemble du trafic HTTPS entrant vers **mail.nebulo.games**.  
Durcissement de la configuration TLS, activation des headers de sécurité et limitation des flux HTTP(S) autorisés.

![Déploiement Nginx](/admin.homelab/assets/images/nginx-deployment.png)

### 🔹 Gestion des certificats public/privé
Importation du certificat SSL correspondant à **mail.nebulo.games**.  
Configuration du serveur virtuel Nginx en mode *TLS offloading* pour centraliser le chiffrement.

![Certificat Nginx](/admin.homelab/assets/images/nginx-certificate.png)

### 🔹 Routage des services Exchange
Configuration précise des règles Nginx pour router les différentes URL Exchange vers **SRV-EXCH01** :  
- OWA / ECP  
- Autodiscover  
- ActiveSync / EWS  
- MAPI over HTTP  

![Routage Nginx Exchange](/admin.homelab/assets/images/nginx-exchange-routing.png)

### 🔹 Sécurisation et filtrage
Application des protections côté reverse proxy :  
- Headers HTTP sécurisés (HSTS, X-Frame-Options, etc.)  
- Limitation du nombre de connexions  
- Protection brute-force basique sur OWA/ECP  
- Filtrage User-Agent et limitation des méthodes HTTP  

![Sécurisation Nginx](/admin.homelab/assets/images/nginx-security.png)

---

## ✔️ Résultats

- Publication externe **sécurisée** de tous les services Exchange  
- Accès **OWA** et **ActiveSync** pleinement opérationnels depuis Internet  
- **Autodiscover** fonctionnel pour les clients Outlook externes  
- Exposition maîtrisée grâce au reverse proxy Nginx en DMZ  
- Architecture robuste, conforme aux recommandations Microsoft  

---

## 🧠 Compétences mises en avant

- Déploiement d’un reverse proxy **Nginx** en DMZ  
- Maîtrise de la publication **HTTPS / TLS** pour services Exchange  
- Architecture réseau multi-zones (DMZ ↔ LAN)  
- Configuration avancée des services Web Exchange (OWA, EWS, MAPI, ActiveSync)  
- Sécurisation HTTP(S) et gestion des certificats  
- Mise en place d’une exposition publique professionnelle sur un domaine externe  

---

## 📎 Ressources associées

[exchange-reverseproxy-deployment.pdf](/admin.homelab/assets/pdfs/exchange-reverseproxy-deployment.pdf)
