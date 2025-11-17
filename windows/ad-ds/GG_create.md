---
title: Procédure - Création GG
parent: Documentation AD DS
nav_order: 5
---

# 👥 Création des Groupes Globaux (GG)

Dans cette étape, nous créons les **Groupes Globaux (GG)** utilisés pour représenter les services ou départements de l’entreprise.  
Ces groupes seront ensuite utilisés dans la méthode **AGDLP** pour gérer les permissions.

Les groupes à créer :

- **GG_Direction**
- **GG_Comptabilité**
- **GG_Secrétariat**
- **GG_Production**
- **GG_Support_informatique**

---

## 1. Ouvrir la console Utilisateurs et ordinateurs Active Directory

1. Ouvrir **Outils d'administration** → **Utilisateurs et ordinateurs Active Directory**.
2. Naviguer vers :  
   **Mon entreprise → Groupes → Services**

**Capture d’écran :**  
![ADUC Services](/admin-homelab/assets/capture/adds/groups_services.png)

---

## 2. Créer un groupe global

1. Clic droit dans le volet central → **Nouveau** → **Groupe**.  
2. Renseigner :  
   - **Nom du groupe :** par exemple `GG_Direction`  
   - **Portée du groupe :** *Global*  
   - **Type de groupe :** *Security*  
3. Cliquer sur **OK**.

**Capture d’écran :**  
![Créer groupe global](/admin-homelab/assets/capture/adds/group_new.png)

---

## 3. Répéter l’opération pour chaque service

Créer les groupes suivants dans la même OU **Services** :

- `GG_Comptabilité`
- `GG_Sécrétariat`
- `GG_Production`
- `GG_Support_informatique`

**Capture d’écran :**  
![Liste groupes globaux](/admin-homelab/assets/capture/adds/groups_list.png)

---

## Étape suivante

## Étape suivante

➡️ Procéder à la **création des utilisateurs** dans l’OU *Utilisateurs*  
(une page dédiée décrira la procédure complète avec captures d’écran)

Une fois les utilisateurs créés, nous passerons ensuite à :

➡️ La création des **Groupes de Domaine Locaux (DL)** dans l’OU *Partages*  
➡️ Puis la mise en place de la méthode **AGDLP**

---
