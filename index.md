---
title: Accueil
description: Landing page
permalink: /
---

# 🧠 Wiki SysAdmin – Cédric Ambos

---

Bienvenue sur mon **Wiki d’administration systèmes et réseaux**.  
Ce projet documente mes déploiements, mes expérimentations et mes connaissances autour des environnements **Windows Server**, **Debian**, et **infrastructures réseau**.

Ce wiki me sert à la fois de :
- 📚 **Documentation technique personnelle**
- 💼 **Portfolio professionnel**
- 🧩 **Laboratoire d’expérimentation**

---

## 📁 Navigation principale

- 💠 [Infrastructure Windows](windows/index.md)
- 🐧 [Infrastructure Debian](debian/)
- 🌐 [Infrastructure réseau & sécurité](infrastructure/)
- 👤 [À propos de moi](about.md)

---

## 🧱 Structure du projet
```
admin-homelab/
├── index.md → Page d’accueil du site
├── about.md → Profil / contact
│
├── windows/ → Services Windows Server
│ ├── ad-ds.md
│ ├── dns.md
│ ├── dhcp.md
│ ├── filesrv.md
│ ├── printsrv.md
│ └── collaboration.md
│
├── debian/ → Services Debian
│ ├── dns.md
│ ├── dhcp.md
│ └── print.md
│
├── infrastructure/ → Réseau, sécurité, outils
│ ├── pfsense.md
│ ├── vlan-segmentation.md
│ ├── glpi.md
│ ├── supervision.md
│ ├── rds.md
│ └── wds.md
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
