---
title: Procédure - Création Utilisateurs
parent: Documentation AD DS
nav_order: 7
---

# 👤 Création des utilisateurs Active Directory

Cette procédure décrit la création des comptes utilisateurs dans l’OU **Utilisateurs** de l’arborescence AD.

---

# 🧩 Création d’un modèle d’utilisateur (Template) par service

L’objectif est de créer un **compte modèle** pour chaque service.  
Ce modèle contiendra :  
- l’appartenance au **Groupe Global (GG)** du service,  
- les informations de base du profil,  
- les paramètres préconfigurés (organisation, description…).

Ensuite, chaque nouveau compte utilisateur du service sera créé par **copie du modèle**, ce qui garantit une configuration cohérente et rapide.

---

## 1. Ouvrir la console Active Directory Users and Computers

1. Ouvrir **Outils d’administration** → **Utilisateurs et ordinateurs Active Directory**  
2. Naviguer vers :  
   **Mon entreprise → Utilisateurs**

**Capture d’écran :**  
![Console AD](/admin-homelab/assets/capture/adds/users_console.png)

---

## 2. Créer le modèle d’utilisateur

1. Clic droit sur **Utilisateurs** → **Nouveau** → **Utilisateur**
2. Nommer le modèle selon le service, par exemple :  
   **modele_direction**

 **Capture d’écran :**  
![Créer modèle AD](/admin-homelab/assets/capture/adds/user_template1.png)

4. Définir un mot de passe simple et cocher :  
   - **Le mot de passe n’expire jamais**  
   - **L’utilisateur ne peut pas changer son mot de passe**
  
**Capture d’écran :**  
![Créer modèle AD](/admin-homelab/assets/capture/adds/user_template2.png)

> Ce compte modèle **ne doit jamais servir à se connecter** : il sert uniquement de structure.

---

## 3. Ajouter le modèle au Groupe Global du service

1. Ouvrir les propriétés du compte **modele_direction**

**Capture d’écran :**  
![Ajouter au GG](/admin-homelab/assets/capture/adds/user_add_group1.png)

2. Aller dans l’onglet **Membre de**

3. Ajouter :  
   - **GG_Direction**

**Capture d’écran :**  
![Ajouter au GG](/admin-homelab/assets/capture/adds/user_add_group2.png)

---

## 4. Répéter pour les autres services

Créer les modèles suivants :

- **modele_comptabilite** → membre de **GG_Comptabilité**  
- **modele_secretariat** → membre de **GG_Sécrétariat**  
- **modele_production** → membre de **GG_Production**  
- **modele_support** → membre de **GG_Support_informatique**

> Tous les modèles sont placés dans :  
> **Mon entreprise → Utilisateurs**

**Capture d’écran :**  
![Liste modèles](/admin-homelab/assets/capture/adds/user_models.png)

---

## 5. Utiliser un modèle pour créer un nouvel utilisateur

Lorsque vous devez créer un utilisateur d’un service :

1. Clic droit sur **modele_direction** → **Copier**

**Capture d’écran :**  
![Copie modèle](/admin-homelab/assets/capture/adds/user_copy1.png)

2. Renseigner les informations du nouvel employé :  
   - Nom  
   - Prénom  
   - Nom d’ouverture de session
  
**Capture d’écran :**  
![Copie modèle](/admin-homelab/assets/capture/adds/user_copy2.png)

3. L’appartenance au groupe **GG_Direction** sera automatiquement copiée  
4. Définir un mot de passe temporaire  
5. Cocher :  
   - **L’utilisateur doit changer le mot de passe à la prochaine ouverture de session**

**Capture d’écran :**  
![Copie modèle](/admin-homelab/assets/capture/adds/user_copy3.png)

---

## 6. Tableau des utilisateurs par service


| Service              | Membres                                                |
|----------------------|--------------------------------------------------------|
| Direction            | Christian Hef, Pauline Atron, Pascaline Résident       |
| Comptabilité         | Bruno Ilan, Christelle Rédit, Florence Acture          |
| Secrétariat          | Cédric Ourrier, Sandrine Tandard, Aline Genda          |
| Production           | Chloé Hâne, Ursule Sine, Denis Elais                   |
| Support Informatique | Clément Lavier, Cédric Ambos, Elodie Cran              |


**Capture d’écran :**  
![Copie modèle](/admin-homelab/assets/capture/adds/all_users.png)

---

## Étape suivante

➡️ Création des **Groupes de Domaine Locaux (DL)** et attribution des permissions  
➡️ Structuration des partages et mise en place de **AGDLP**

---
