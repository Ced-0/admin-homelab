---
title: Procédure - Création OU
parent: Documentation AD DS
nav_order: 5
---

# 📁 Création de l’arborescence Active Directory (OU)

---

Cette procédure décrit la mise en place de l’arborescence d’Unités d’Organisation (OU) utilisée dans mon homelab, conformément aux bonnes pratiques AD DS.

---

## 1. Ouvrir la console Active Directory Users and Computers

1. Ouvrir **Outils d'administration** → **Utilisateurs et ordinateurs Active Directory**.  
2. Se placer à la racine du domaine.

**Capture d’écran :**  
![OU Console](/admin-homelab/assets/capture/adds/ou_console.png)

---

## 2. Créer l’OU principale : *Mon entreprise*

1. Clic droit sur le domaine → **Nouveau** → **Unité d'organisation**.  
2. Nommer l’OU : **Mon entreprise**.  
3. Valider.

**Capture d’écran :**  
![Créer OU Mon entreprise](/admin-homelab/assets/capture/adds/ou_main.png)

---

## 3. Créer les sous-OU principales

À l’intérieur de **Mon entreprise**, créer les OU suivantes :

- **Groupes**  
- **Ordinateurs**  
- **Utilisateurs**

**Capture d’écran :**  
![Créer sous OU](/admin-homelab/assets/capture/adds/ou_sub.png)

---

## 4. Création des OU Groupes

### 4.1 OU *Partages*  
Destinée aux groupes utilisés pour les droits NTFS/SMB (méthode AGDLP).

### 4.2 OU *Services*  
Destinée aux groupes liés aux services internes (IT, RH, Finance…).

**Capture d’écran :**  
![Créer OU Services](/admin-homelab/assets/capture/adds/ou_groups.png)

---

## 5. Création des OU Ordinateurs

### 5.1 OU *Clients*  
Pour les postes utilisateurs.

### 5.2 OU *Serveurs*  
Pour les machines serveurs du domaine.

**Capture d’écran :**  
![OU Ordinateurs](/admin-homelab/assets/capture/adds/ou_computers.png)

---

## 6. OU Utilisateurs

Cette OU regroupe l’ensemble des comptes utilisateurs finaux (hors comptes administratifs si souhaité).

---

## 7. Arborescence complète attendue

Voici l’arborescence complète :
```
Mon entreprise
│
├── Groupes
│   ├── Partages
│   └── Services
│
├── Ordinateurs
│   ├── Clients
│   └── Serveurs
│
└── Utilisateurs
```

**Capture d’écran :**  
![Arborescence AD](/admin-homelab/assets/capture/adds/ou_tree.png)

---

## Étape suivante

➡️ Procéder à la **création des utilisateurs**, **groupes**, et **attribution des permissions**, selon la méthode AGDLP.  
(Une page dédiée détaillera ces étapes.)

---
