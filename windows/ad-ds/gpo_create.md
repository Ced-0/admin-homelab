---
title: Procédure - Création GPO
parent: Documentation AD DS
nav_order: 9
---

# 🛡️ Gestion des GPO (Group Policy Objects)

Cette page décrit la création, la gestion et l’application des **stratégies de groupe (GPO)** dans un environnement Active Directory.  
Les GPO permettent de configurer automatiquement les postes clients : sécurité, restrictions, déploiement de logiciels, scripts, configuration réseau, etc.

---

# 1. Ouvrir la console Gestion des stratégies de groupe (GPMC)

1. Aller dans **Outils d'administration**
2. Cliquer sur **Gestion de la stratégie de groupe**

![Console GPMC](/admin-homelab/assets/capture/adds/gpmc_console.png)

---

# 2. Structure des GPO

Dans la console, on distingue :

- **Objets de stratégie de groupe** → contient toutes les GPO du domaine  
- **Forêt / Domaine / OU** → où sont liées les GPO  
- **Filtres WMI / Sécurité** → filtres d'application  

![Structure GPMC](/admin-homelab/assets/capture/adds/gpmc_structure.png)

---

# 3. Créer une nouvelle GPO

1. Clic droit sur l’OU cible  
2. Sélectionner : **Créer un objet GPO dans ce domaine et le lier ici**
3. Nommer la GPO (ex : `GPO_Verouillage_Ecran`)

![Créer GPO](/admin-homelab/assets/capture/adds/create_gpo.png)

---

# 4. Modifier une GPO

1. Clic droit sur la GPO → **Modifier**
2. L’éditeur s’ouvre avec deux sections :

### 🔧 Configuration ordinateur  
Paramètres appliqués **au poste** avant ouverture de session.

### 👤 Configuration utilisateur  
Paramètres appliqués **à l’utilisateur**.

![Modifier GPO](/admin-homelab/assets/capture/adds/edit_gpo.png)

---

# 5. Exemple : verrouillage automatique

1. Éditer la GPO  
2. Aller dans :  
   `Configuration utilisateur → Modèles d'administration → Panneau de configuration → Personnalisation`

Configurer :

- **Activer l'écran de veille** → *Activé*  
- **Empêcher de modifié l'écran de veille** → *Activé*
- **Dépassement du délai d'expiration de l'écran de veille** → *600 secondes (10 min)* → *Activé*  

![Screensaver GPO](/admin-homelab/assets/capture/adds/screensaver.png)

---

# 6. Exemple : fond d’écran d’entreprise

1. Ajouter le fichier sur un partage :  
   `\\SRV-FIC\Outils$\GPO_Ressources\wallpaper.jpg`

2. Modifier la GPO :  
   `Configuration utilisateur → Modèles d’administration → Bureau → Active Desktop`

Paramètres :

- **Papier peint du Bureau** : chemin UNC  
- Mode d’affichage : *Ajusté / Centré / Étendu*

![Wallpaper GPO](/admin-homelab/assets/capture/adds/wallpaper.png)

---

# 7. Tester les GPO sur un poste Windows

### Forcer la mise à jour
```
gpupdate /force
```

### 📋 Vérifier les GPO appliquées
```
gpresult /r
```

### Rapport HTML
```
gpresult /h gpo-report.html
```

![gpresult](/admin-homelab/assets/capture/adds/gpresult.png)

---

# 8. Ordre d’application des GPO (LsPd)

Les GPO s'appliquent dans cet ordre :

1. **L**ocal  
2. **S**ite  
3. **P**arcours de domaine (Domaine)  
4. **d**'OU (de la racine vers la feuille)

La dernière GPO appliquée l’emporte, sauf si :

- **Appliqué (Enforced)** est activé

![Héritage GPO](/admin-homelab/assets/capture/adds/inheritance1.png)

- L’OU **bloque l’héritage**  

![Héritage GPO](/admin-homelab/assets/capture/adds/inheritance2.png)

---

# 9. Filtrage des GPO

## Par groupes de sécurité

1. Ouvrir **Délégation / Sécurité**
2. Retirer *Authenticated Users*
3. Ajouter un groupe (ex : `GG_Production`)

![Filtrage](/admin-homelab/assets/capture/adds/filter_add.png)

---

# 10. GPO utilisées pour mon homelab

| Catégorie  | Nom GPO                   | Description                                 |
|-----------|---------------------------|----------------------------------------------|
| Sécurité  | Default Domain Policy     | Mots de passe (default Domain Policy)        |
| Bureau    | GPO_Fond_Ecran            | Fond d'écran                                 |
| Sécurité  | GPO_Verouillage_ecran     | Veille et verrouillage auto                  |
| Scripts   | GPO_Map_Partages          | Mappage automatique des lecteurs réseaux     |
| Scripts   | GPO_Map_Imprimantes       | Mappage automatique des imprimantes          |

---

# Étape suivante

➡️ Nous passons à la section **DNS**  

---
