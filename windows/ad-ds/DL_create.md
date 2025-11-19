---
title: Procédure - Création DL
parent: Documentation AD DS
nav_order: 8
---

# 🛡️ Création des Groupes de Domaine Locaux (DL)

Dans cette étape, nous créons les **Groupes de Domaine Locaux (DL)** associés directement aux **dossiers partagés** de l’infrastructure.  
Ces groupes recevront les permissions NTFS/SMB qui seront ensuite attribuées aux **Groupes Globaux (GG)** selon la méthode **AGDLP**.

---

## 📁 Dossiers partagés existants

Les partages configurés dans mon homelab sont :

```
DATA  *(Accès Lecture pour tout le monde)*
│
├── Services  *(Accès Lecture pour tout le monde)*
│   ├── direction  *(Accès Modification pour la direction et comptabilité - Lecture pour les secrétaires)*
│   ├── comptabilité  *(Accès Modification pour les comptables - Lecture pour la direction et les secrétaires)*
│   ├── secrétariat  *(Accès Modification pour tous les secrétaires)*
│   └── support  *(Accès Modification pour le support et les secrétaires - Lecture pour la direction)*
│
├── Public  *(Accès Modification pour tout le monde)*
│
└── Informatique  *(dossier et partage caché — Accès Modification pour le service informatique)*
```

Les DL créés correspondront exactement à ces dossiers.

---

# 1. Convention de nommage utilisée
```
DL_<NomDuDossier>_<Droit>
```

---

# 2. Ouvrir la console Utilisateurs et ordinateurs Active Directory

1. Ouvrir **Outils d'administration** → **Utilisateurs et ordinateurs Active Directory**  
2. Naviguer vers :  
   **Mon entreprise → Groupes → Partages**

**Capture d’écran :**  
![OU Partages](/admin-homelab/assets/capture/adds/groups_partages.png)

---

# 3. Créer un groupe de domaine local

1. Clic droit dans l’OU **Partages** → **Nouveau** → **Groupe**  
2. Renseigner :  
   - **Nom du groupe :** `DL_DATA_RO` *(exemple)*  
   - **Portée du groupe :** Domaine local  
   - **Type du groupe :** Sécurité  
3. Cliquer sur **OK**

**Capture d’écran :**  
![Créer DL](/admin-homelab/assets/capture/adds/group_dl_new.png)

---

# 4. Créer tous les DL correspondant aux partages

Créer les groupes suivants dans l’OU **Partages** :

| Dossier partagé   | Groupe DL à créer                                      |
|-------------------|--------------------------------------------------------|
| DATA              | `DL_DATA_RO`, `DL_DATA_RW`                             |
| SERVICES          | `DL_SERVICES_RO`, `DL_SERVICES_RW`                     |
| DIRECTION         | `DL_DIRECTION_RO`, `DL_DIRECTION_RW`                   |
| COMPTABILITE      | `DL_COMPTABILITE_RO`, `DL_COMPTABILITE_RW`             |
| SECRETARIAT       | `DL_SECRETARIAT_RO`, `DL_SECRETARIAT_RW`               |
| SUPPORT           | `DL_SUPPORT_RO`, `DL_SUPPORT_RW`                       |
| PUBLIC            | `DL_PUBLIC_RO`, `DL_PUBLIC_RW`                         |
| INFORMATIQUE      | `DL_INFORMATIQUE_RO`, `DL_INFORMATIQUE_RW`             |
| UTILISATEURS      | *(pas de DL global — droits individuels)*              |

⚠️ **J'ai choisi de créer des groupes de Read-Only (RO) et Read-Write (RW)** pour chaque dossier, assurant ainsi une **standardisation des permissions** à travers tous les répertoires.

Cependant, **ce n'est pas forcément nécessaire ni recommandé**. On pourra se limiter au **Domain Local (DL)** strictement nécessaire en fonction de la politique de l'entreprise.

**Capture d’écran :**  
![Liste DL](/admin-homelab/assets/capture/adds/groups_dl_list.png)

---

# 5. Ajouter les Groupes Globaux (GG) aux DL

1. Ouvrir les propriétés du groupe DL (double-clic).  
2. Onglet **Membres** → **Ajouter**.  
3. Rechercher et ajouter le groupe global correspondant, par ex. `GG_Direction` dans `DL_DIRECTION_RW`.
4. Valider.

**Capture d’écran :**  
![Ajout GG](/admin-homelab/assets/capture/adds/add_gg.png)

---

# Étape suivante

➡️ Associer chaque **GG** au **DL** correspondant (méthode AGDLP)  
➡️ Appliquer les droits **NTFS/SMB** sur les dossiers partagés

---
