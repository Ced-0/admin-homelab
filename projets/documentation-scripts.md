---
title: Documentation et Scripts
parent: Projets
nav_order: 20
---

# Documentation et Scripts

Cette page centralise tous les **scripts et automatisations** utilisés dans le lab pour l’administration, le déploiement et la supervision des services. L’objectif est de fournir un référentiel complet et exploitable pour la maintenance ou la réplication du lab.

---

## 🎯 Objectifs

- Centraliser tous les scripts utilisés pour le lab (PowerShell, Bash, PfSense, monitoring)  
- Documenter l’usage, les paramètres et exemples d’exécution  
- Fournir un référentiel pour automatiser les tâches récurrentes  
- Ajouter des PDF et captures pour scripts critiques  

---

## 🖥️ Organisation générale (structure logique)

La page est organisée par type de script et usage, mais **tout est sur la même page** :  

- **PowerShell** → AD, File Server, Print Server, Exchange, WAPT  
- **Bash / Linux** → GLPI, Xivo, DNS sync  
- **PfSense** → VLAN et firewall rules  
- **Monitoring / Supervision** → Zabbix agents Windows et Linux  

Chaque section contient :  
1. Exemples de scripts  
2. Placeholders pour screenshots ou PDF  

---

## 💻 Scripts PowerShell

### AD / File / Print

```powershell
# Création d'un utilisateur AD
New-ADUser -Name "cmartin" `
           -GivenName "Claire" `
           -Surname "Martin" `
           -SamAccountName "cmartin" `
           -AccountPassword (ConvertTo-SecureString "Mdp123!" -AsPlainText -Force) `
           -Enabled $true `
           -Path "OU=HR,DC=corp,DC=local"
powershell
Copier le code
# Configuration permissions File Server
.\file-server-permissions.ps1
powershell
Copier le code
# Setup imprimantes réseau
.\print-server-setup.ps1
PDF / capture : AD & File Server Scripts
Screenshot placeholder :

Exchange & WAPT
powershell
Copier le code
# Exchange Server interne
.\exchange-setup.ps1

# Déploiement WAPT
.\wapt-deploy.ps1
PDF / capture : Exchange & WAPT Scripts
Screenshot placeholder :

🐚 Scripts Bash / Linux
bash
Copier le code
#!/bin/bash
# Backup GLPI
tar -czvf /backup/glpi_$(date +%F).tar.gz /var/www/glpi/

# Backup Xivo
tar -czvf /backup/xivo_$(date +%F).tar.gz /etc/xivo/

# Synchronisation DNS Debian → Windows
./dns-sync.sh
PDF / capture : Backup & DNS Scripts
Screenshot placeholder :

🔧 Scripts PfSense
bash
Copier le code
#!/bin/bash
# Création VLAN sur interface LAN
pfSsh.php playback interface_vlan_add LAN 50 "VLAN50-Services" 50

# Import/Export règles firewall
pfSsh.php playback rules_import /configs/firewall-rules.conf
PDF / capture : PfSense Scripts
Screenshot placeholder :

📊 Scripts Monitoring / Supervision
powershell
Copier le code
# Installation agent Zabbix Windows
.\zabbix-agent-install.ps1
bash
Copier le code
# Installation agent Zabbix Linux
./zabbix-agent-install.sh
PDF / capture : Zabbix Agents Scripts
Screenshot placeholder :

✅ Bonnes pratiques
Commenter chaque script pour expliquer l’objectif et les paramètres

Tester chaque script dans un environnement de lab avant production

Stocker les scripts sur le serveur de documentation et versionner si possible (Git)

Sécuriser les scripts contenant des mots de passe ou clés sensibles

📄 Placeholder PDF ou capture finale Scripts
scripts-documentation.pdf