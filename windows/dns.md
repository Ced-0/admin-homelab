# Création d’une zone DNS indépendante : *demo.infra*

Cette page présente la création d’une zone DNS **hors Active Directory**, utilisée pour illustrer la gestion d’enregistrements DNS dans un environnement Windows Server.

La zone *demo.infra* sert de **terrain de démonstration** pour montrer :  

- la création d’une zone primaire non intégrée à AD  
- l’ajout d’enregistrements A, CNAME et MX  
- la gestion d’un mini-espace DNS cohérent  
- l’utilisation des redirecteurs conditionnels

---

# 1. Création de la zone *demo.infra*

1. Ouvrir **DNS Manager**  
2. Clic droit sur **Zones de recherche directe**  
3. Sélectionner **Nouvelle zone…**  
4. Choisir :  
   - **Zone principale**  
   - **Ne pas stocker dans Active Directory**  
   - Nom de zone : **demo.infra**  
   - Fichier de zone : *demo.infra.dns*

**Capture d’écran :**  
![Nouvelle zone DNS](/admin-homelab/assets/capture/dns/demo_zone_create.png)

**Capture d’écran (choix zone principale)**  
![Type zone](/admin-homelab/assets/capture/dns/demo_zone_type.png)

---

# 2. Ajout d’une zone inverse (in-addr.arpa) pour la démo

# 3. Structure de la zone *demo.infra*

La zone contient des enregistrements **mixtes (réels et fictifs)** afin de démontrer différentes possibilités d'administration DNS.

---

## 2.1. Enregistrements A (hôtes)

| Nom | Type | IP | Description |
|------|------|------|-----------------------------|
| srv-dns | A | 172.20.10.10 | Serveur DNS réel de la zone |
| web | A | 172.20.10.20 | Service Web interne (exemple) |
| nas | A | 172.20.10.30 | NAS interne fictif |
| app | A | 172.20.10.40 | Application interne fictive |

**Capture d’écran :**  
![Enregistrements A](/admin-homelab/assets/capture/dns/demo_a_records.png)

---

## 3.2. Alias (CNAME)

| Nom | Type | Cible |
|------|------|------------------------------|
| files | CNAME | nas.demo.infra |
| portail | CNAME | web.demo.infra |

**Capture d’écran :**  
![CNAME](/admin-homelab/assets/capture/dns/demo_cname_records.png)

---

## 3.3. Enregistrements MX (serveur mail fictif)

Même si tu n’as pas de serveur mail, cet enregistrement montre ta compréhension du rôle MX.

| Nom | Type | Valeur |
|------|------|---------------------------|
| demo.infra | MX | 10 mail.demo.infra |
| mail | A | 172.20.10.15 |

**Capture d’écran :**  
![MX](/admin-homelab/assets/capture/dns/demo_mx_records.png)

---

# 4. Redirecteur conditionnel vers *demo.infra*

Tu peux créer un redirecteur conditionnel sur un **autre serveur DNS** de ton homelab pour montrer la résolution externe de zone interne.

1. Ouvrir DNS Manager  
2. Clic droit sur **Redirecteurs conditionnels**  
3. Ajouter : **demo.infra**  
4. IP du serveur : **172.20.10.10**

**Capture d’écran :**  
![Redirecteur conditionnel](/admin-homelab/assets/capture/dns/demo_forwarder.png)

---

# 5. Tests de résolution DNS

Tests simples :

```powershell
nslookup web.demo.infra
nslookup files.demo.infra
nslookup -type=mx demo.infra
nslookup 172.20.10.20
```

Capture d’écran :

# 6. Résultat final de la zone

```
demo.infra
├── srv-dns       A      172.20.10.10
├── web           A      172.20.10.20
├── nas           A      172.20.10.30
├── app           A      172.20.10.40
├── files         CNAME  nas.demo.infra
├── portail       CNAME  web.demo.infra
├── mail          A      172.20.10.15
└── demo.infra    MX     10 mail.demo.infra
```

---

# Étape suivante

➡️ Intégration de la zone demo.infra dans un scénario complet

---
