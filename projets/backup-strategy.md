---
title: Stratégie de Sauvegarde
parent: Projets
nav_order: 19
---

# Stratégie de Sauvegarde

Cette page décrit la mise en place de la **stratégie de sauvegarde** pour tous les serveurs et services critiques du lab. L’objectif est de garantir la récupération des données en cas d’incident ou de panne.

---

## 🎯 Objectifs

- Définir une stratégie de sauvegarde **complète et régulière** pour tous les serveurs  
- Sauvegarder les **services critiques** : AD, File Server, Print Server, Exchange, GLPI, Xivo  
- Utiliser différents outils selon le type de serveur : Bacula, Borg/Veeam  
- Isoler les backups sur VLAN dédié (VLAN 90) pour sécurité  
- Préparer la récupération rapide des services  

---

## 🖥️ Architecture Backup

| Serveur / Service       | Solution            | VLAN / IP       | Notes |
|------------------------|-------------------|----------------|-------|
| SRV-FILE01             | Veeam / Bacula    | VLAN 90        | Sauvegarde des partages fichiers |
| SRV-PRINT01            | Veeam / Bacula    | VLAN 90        | Sauvegarde des configurations d’imprimantes |
| SRV-GLPI01             | Borg / Backup     | VLAN 90        | Sauvegarde base GLPI + fichiers |
| SRV-EXCH01             | Veeam / Bacula    | VLAN 90        | Sauvegarde boîtes Exchange et DB |
| SRV-XIVO01             | Borg / Backup     | VLAN 90        | Sauvegarde configuration Xivo |
| SRV-AD01 / SRV-AD02    | System State / Veeam | VLAN 90     | Sauvegarde des contrôleurs de domaine |

**Diagramme logique Backup :**  
![Diagramme Backup](images/backup-architecture.png)

---

## 🔧 Configuration et mise en place

### 1️⃣ Bacula / Veeam

- Installer les agents sur tous les serveurs Windows et Linux  
- Configurer les jobs de sauvegarde planifiés (quotidien, hebdomadaire, mensuel)  
- Définir les politiques de rétention selon criticité des données  

### 2️⃣ Borg (Linux)

- Installer Borg sur serveurs Linux (GLPI, Xivo)  
- Créer des **archives chiffrées** pour sécuriser les données  
- Stocker les backups sur VLAN dédié (NAS / serveur backup)  

### 3️⃣ Sécurisation et isolation

- VLAN 90 dédié pour tous les backups  
- Restreindre l’accès aux seuls administrateurs IT  
- Chiffrement des sauvegardes sensibles (AD, Exchange, Finance, RH)  

### 4️⃣ Vérification et tests

- Restaurer des fichiers tests pour valider les sauvegardes  
- Vérifier les logs et alertes des jobs de sauvegarde  
- Simuler un scénario de panne pour tester la récupération complète  

---

## ✅ Vérification

- Tous les serveurs critiques disposent d’une sauvegarde fonctionnelle  
- Les restaurations de test sont réussies  
- Les sauvegardes sont isolées et sécurisées sur VLAN 90  
- Les alertes sont configurées pour prévenir en cas d’échec  

---

## 🖼️ Placeholder image / screenshot Backup

![Backup Dashboard](images/backup-dashboard.png)

---

## 📄 Placeholder PDF ou capture finale Backup

[backup-strategy.pdf](pdfs/backup-strategy.pdf)
