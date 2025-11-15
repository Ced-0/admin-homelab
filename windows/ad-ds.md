---
title: "AD DS"
layout: single
sidebar:
  nav: "navigation"
permalink: /windows/ad-ds/
---

# Active Directory Domain Services (AD DS)

## 🎯 Objectif de la page
Présenter ce qu’est Active Directory, expliquer ses rôles, détailler son fonctionnement et montrer des exemples de tâches administratives *réalistes* que je peux effectuer en tant qu’administrateur système junior.

---

## 📌 Qu’est-ce que Active Directory Domain Services ?

Active Directory Domain Services (AD DS) est un service de rôle Windows Server permettant de :

- Centraliser la gestion des utilisateurs, groupes, ordinateurs et ressources.
- Contrôler l’authentification via Kerberos/NTLM.
- Déployer des stratégies de sécurité (GPO).
- Structurer une organisation avec domaines, arbres et forêts.
- Assurer la résolution de noms internes grâce à DNS intégré.

AD DS est un élément fondamental dans toute infrastructure Windows professionnelle.

---

## 🧱 Composants clés

### **1. Domaine (Domain)**
Un domaine est une limite administrative.  
Exemple :  
`entreprise.local`

### **2. Contrôleur de domaine (Domain Controller – DC)**
Serveur qui héberge AD DS.  
Il contient la base **NTDS.dit** et authentifie les utilisateurs.

### **3. Unités d’Organisation (OU)**

```

entreprise.local
├── Utilisateurs
├── Groupes
├── Ordinateurs
└── Services

```

### **4. Objets**
- Utilisateurs  
- Groupes  
- Ordinateurs  
- Partages de fichiers  
- Imprimantes

### **5. Group Policy Objects (GPO)**
Permettent de gérer :
- sécurité (verrouillage session, firewall…)
- configuration des postes
- installation de logiciels

---
