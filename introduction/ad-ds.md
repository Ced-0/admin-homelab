---
title: AD DS
parent: Introduction
nav_order: 1
---

# Active Directory Domain Services (AD DS)

## Introduction

Active Directory Domain Services (AD DS) est l’un des composants centraux d’une infrastructure Windows Server. Il permet de centraliser l’authentification, la gestion des utilisateurs, des ordinateurs et des ressources d’un réseau. Grâce à AD DS, les organisations peuvent appliquer des stratégies uniformes, renforcer la sécurité et structurer efficacement leur environnement informatique.

---

## 📌 Rôle et objectifs d’Active Directory

AD DS assure plusieurs fonctions essentielles :

- **Authentification centralisée** : contrôle l’accès aux ressources via un annuaire sécurisé.
- **Gestion des identités** : administration des utilisateurs, groupes, ordinateurs et permissions.
- **Organisation hiérarchique** : structure logique basée sur les domaines, les forêts et les unités d’organisation.
- **Application de stratégies réseau** : déploiement des règles et configurations grâce aux GPO (Group Policy Objects).
- **Intégration DNS** : prise en charge de la résolution de noms et de la localisation des services internes.

---

## 🧱 Les composants fondamentaux

### **1. Domaine (Domain)**
Le domaine représente l’unité de base d’Active Directory.  
Il regroupe et sécurise comptes, ressources et stratégies au sein d’une entité administrative.

Exemple :  
`entreprise.local`

### **2. Contrôleur de domaine (Domain Controller)**
Le contrôleur de domaine héberge la base d’annuaire et répond aux demandes d’authentification.  
Il joue un rôle essentiel dans la cohérence et la disponibilité du système.

### **3. Unités d’Organisation (OU)**
Les OU servent à structurer l’annuaire pour organiser les objets selon une logique métier.
```
entreprise.local
├── Utilisateurs
├── Groupes
├── Ordinateurs
└── Services
```

### **4. Objets AD**
L’annuaire contient plusieurs types d’objets :

- Utilisateurs  
- Groupes  
- Ordinateurs  
- Ressources partagées  
- Imprimantes  

Chaque objet possède des attributs et des règles permettant de le contrôler.

### **5. Group Policy Objects (GPO)**
Les GPO permettent d’appliquer automatiquement des paramètres et politiques sur les utilisateurs et les ordinateurs, garantissant une configuration homogène et sécurisée.

---

## 🩺 Pourquoi AD DS est indispensable ?

- Il centralise la gestion du réseau.  
- Il garantit une sécurité homogène et cohérente.  
- Il réduit les risques d’erreur grâce à l’automatisation.  
- Il simplifie l’administration quotidienne des postes et comptes.  
- Il offre une vision claire et structurée de l’infrastructure informatique.  

---

## 📑 Ce que j’ai déjà réalisé dans mon Homelab (Portfolio)

- Mise en place d’un domaine complet pour simuler une PME.  
- Création d’une arborescence logique avec plusieurs unités d’organisation.  
- Ajout et gestion de différents types d’objets (utilisateurs, groupes, machines).  
- Application de stratégies de sécurité via les GPO.  
- Intégration de postes clients pour tester l’authentification et la gestion centralisée.

---
