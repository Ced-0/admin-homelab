---
title: Contournement du CGNAT avec VPS
parent: Projets
nav_order: 12
---

# 🌐 Contournement du CGNAT — VPS, Tunnel WireGuard et Relais SMTP/Mailgun

Déploiement d’une architecture permettant de publier correctement les services Exchange vers Internet malgré les restrictions du **CGNAT**, empêchant l’obtention d’une IP publique fixe.  
Pour contourner cette limitation, un **VPS public** a été utilisé comme point d’entrée, associé à un **tunnel WireGuard**, un **relais SMTP** et un **webhook Mailgun** pour assurer la réception et l’envoi des emails externes.

---

## 🎯 Objectifs

- Contourner les limitations du CGNAT empêchant la publication d’Exchange  
- Obtenir une adresse IP publique exploitable pour *nebulo.games*  
- Mettre en place un tunnel WireGuard entre le VPS et Pfsense 
- Traiter les mails entrants Mailgun via requêtes POST  
- Rediriger les mails entrants vers Exchange Edge Transport  

---

## 🖥️ Architecture globale

| Composant            | Rôle                                      | Localisation  |
|----------------------|-------------------------------------------|---------------|
| VPS Public (IONOS)   | IP publique, Nginx, relais SMTP, Python   | Cloud         |
| SRV-EXCH-EDGE        | Exchange Edge Transport                   | DMZ           |
| SRV-EXCH01           | Exchange interne                          | LAN           |

**Diagramme logique :**  
![Architecture CGNAT / VPS / Mailgun](/admin-homelab/assets/images/cgnat-vps-architecture.png)

---

## 🔧 Mise en œuvre

### 🔹 Mise en place du VPS public  

Déploiement d’un VPS Linux disposant d’une IP publique.  
Installation des services nécessaires :  
- Nginx  
- WireGuard  
- Application Python (Flask + Gunicorn)  

![VPS Network / WireGuard](/admin-homelab/assets/images/vps-wireguard-status.png)

---

### 🔹 Tunnel sécurisé WireGuard (VPS ↔ DMZ)

Configuration d’un tunnel chiffré permettant d’acheminer :  
- les flux SMTP entrants vers Edge Transport  
- les mails sortants Exchange via le relais VPS  
- les flux complémentaires HTTPS si nécessaire

![WireGuard Config](/admin-homelab/assets/images/wireguard-config.png)

---

### 🔹 Redirection SMTP sortante (wg0 → interface publique)

Pour contourner le CGNAT, une règle de routage et de NAT a été mise en place afin de :

- recevoir le trafic SMTP provenant du tunnel **wg0**  
- le sortir sur l’interface publique **ens6**  
- réécrire la source avec l’IP publique du VPS (masquerading)  

Ce mécanisme permet à Exchange d'envoyer des mails externes via une IP publique valable.

![Redirection SMTP VPS](/admin-homelab/assets/images/vps-smtp-nat.png)

---

### 🔹 Réception des mails entrants via Mailgun (Webhook POST)

Mailgun transmet les emails entrants en HTTP POST sur le VPS.  
Une application Python (Flask) reçoit les données, reconstruit l’email et l’envoie en SMTP vers Edge Transport.

Le service est exécuté via Gunicorn + systemd.

![Python Gunicorn Service](/admin-homelab/assets/images/mailgun-gunicorn.png)

---

### 🔹 Injection dans Exchange via Edge Transport

Les emails sont transmis via WireGuard en SMTP vers Exchange Edge Transport, qui les traite ensuite normalement via EdgeSync.

![Exchange Edge Mail Flow](/admin-homelab/assets/images/exchange-edge-mailflow.png)

---

## ✔️ Résultats

- Contournement complet des restrictions CGNAT  
- IP publique fiable via VPS  
- Flux SMTP entrants et sortants fonctionnels  
- Tunnel WireGuard stable entre le VPS et Pfsense  
- Intégration propre entre Mailgun et Edge Transport  

---

## 🧠 Compétences mises en avant

- Gestion avancée sous CGNAT  
- Déploiement d’un VPS comme point d’entrée sécurisé  
- Mise en place de tunnels WireGuard  
- Intégration Mailgun via Webhooks POST  
- Développement Python pour reconstruction et forwarding d’emails  
- Architecture DMZ / LAN sécurisée  

---

## 📎 Ressources associées

[mailgun-webhook-code.py](/admin-homelab/assets/files/mailgun-webhook-code.py)  
[cgnat-vps-mailflow.pdf](/admin-homelab/assets/pdfs/cgnat-vps-mailflow.pdf)
