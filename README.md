# 🧠 Wiki SysAdmin – Cédric Ambos

Bienvenue sur mon **Wiki d’administration systèmes et réseaux**.  
Ce projet documente mes déploiements, mes expérimentations et mes connaissances autour des environnements **Windows Server**, **Debian**, et **infrastructures réseau**.

Ce wiki me sert à la fois de :
- 📚 **Documentation technique personnelle**
- 💼 **Portfolio professionnel**
- 🧩 **Laboratoire d’expérimentation**

---

## 🌐 Accès au site

👉 [**Consulter le Wiki en ligne**](https://ced-0.github.io/admin-homelab/)  
*(hébergé avec GitHub Pages)*

---

## 🧱 Structure du projet
```
admin-homelab/
├── index.md → Page d’accueil du site
├── about.md → Profil / contact
│
├── projets/
│   ├── index.md                              # Introduction + méthodologie + contraintes (Hyper-V local)
│   │
│   ├── 01-logical-vlan-architecture.md       # 1 - Architecture réseau logique (VLANs documentés)
│   ├── 02-pfsense-firewall.md                # 2 - Installation PfSense (routing + segmentation logique)
│   │
│   ├── 03-ad-infrastructure.md               # 3 - ADDS + File Server + Print Server + GPO/Hardening
│   │
│   ├── 04-dns-demo-infra.md                  # 4 - DNS Debian → Windows (zone demo.infra)
│   ├── 05-dhcp-mixte.md                      # 5 - DHCP Windows + ISC Debian
│   │
│   ├── 06-pki-internal.md                    # 6 - PKI interne (certificats domaine)
│   ├── 07-wapt-deployment.md                 # 7 - Déploiement et gestion logicielle (WAPT)
│   │
│   ├── 08-glpi-install.md                    # 8 - Installation GLPI + agents
│   ├── 09-antivirus-central.md               # 9 - Serveur antivirus centralisé
│   │
│   ├── 10-exchange-deployment.md             # 10 - Exchange Server interne
│   ├── 11-exchange-edge-dmz.md               # 11 - Exchange Edge en DMZ (DMZ virtuelle)
│   │ 
│   ├── 12-Contournement-cgnat.md             # 12 - VPS Cloud
│   ├── 13-reverse-proxy.md                   # 13 - Reverse Proxy (Exchange OWA,autodiscover)
│   │
│   ├── 14-rds-deployment.md                  # 14 - RDS + RD Gateway + Broker
│   │  
│   ├── 15-free-pbx.md                       # 15 - FreePBX VoIP (architecture logique voix)
│   │
│   ├── 16-syslog-setup.md                    # 16 - Centralisation Syslog
│   ├── 17-zabbix-monitoring.md               # 17 - Supervision Zabbix complète
│   │
│   ├── 18-network-security.md                # 18 - Sécurité réseau, firewall rules, DMZ logique
│   │
│   ├── 19-backup-strategy.md                 # 19 - Stratégie de sauvegarde (Bacula/Borg/Veeam)
│   └── 20-documentation-scripts.md           # 20 - Scripts (PowerShell, Bash, PfSense, automatisation)
│
└── _config.yml → Configuration GitHub Pages
```
---

## 🧰 Technologies utilisées

- **Windows Server 2022**
- **Debian 12 Bookworm**
- **pfSense** (pare-feu et routage)
- **PowerShell** pour l’automatisation
- **Centreon / GLPI** pour la supervision et la gestion IT
- **GitHub Pages + Markdown (Jekyll)** pour la documentation

---

## 📌 Objectifs du wiki

- Créer un **guide complet d’installation et de configuration** pour chaque service
- Centraliser les **bonnes pratiques** et les **procédures internes**
- Faciliter le partage et la réutilisation de configurations dans d’autres environnements

---

## 💡 Exemple de sujets couverts

- 🪟 **Active Directory** : gestion des utilisateurs, GPO, réplication  
- 🐧 **DHCP sous Debian** : configuration, réservations, logs  
- 🔒 **pfSense et VLAN** : segmentation réseau, règles de sécurité  
- 🧰 **GLPI / Centreon** : inventaire et supervision  
- ☁️ **RDS / WDS / Exchange** *(à venir)*  

---

## 📬 Contact

📧 cedric.ambos@gmail.com  
💼 [LinkedIn](https://linkedin.com/in/cedric-ambos)  
🐙 [GitHub](https://github.com/Ced-0)

---

🧾 *Ce wiki est une documentation technique personnelle, créée à des fins d’apprentissage et de démonstration professionnelle.*  
© 2025 Cédric Ambos – Licence MIT

