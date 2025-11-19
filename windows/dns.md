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
   - Nom de zone : **demo.infra**  
   - Fichier de zone : *demo.infra.dns*

**Capture d’écran :**  
![Nouvelle zone DNS](/admin-homelab/assets/capture/dns/demo_zone_create.png)

**Capture d’écran (choix zone principale)**  
![Type zone](/admin-homelab/assets/capture/dns/demo_zone_type.png)

---

# 2. Ajout d’une zone inverse (in-addr.arpa) pour la démo

1. Ouvrir **DNS Manager**  
2. Clic droit sur **Zones de recherche inversée**  
3. Sélectionner **Nouvelle zone…**  

**Capture d’écran :**  
![Nouvelle zone inverse](/admin-homelab/assets/capture/dns/demo_reverse_create.png)

# 3. Structure de la zone *demo.infra*

La zone contient des enregistrements **mixtes (réels et fictifs)** afin de démontrer différentes possibilités d'administration DNS.

---

## 2.1. Enregistrements A (hôtes)

| Nom | Type | IP | Description |
|------|------|------|-----------------------------|
| srv-dns1 | A | 192.168.100.103 | Serveur DNS Principal |
| srv-dns2 | A | 192.168.100.110 | Serveur DNS Secondaire |
| web | A | 192.168.100.20 | Service Web interne (exemple) |
| nas | A | 192.168.100.30 | NAS interne fictif |
| app | A | 192.168.100.40 | Application interne fictive |

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
| mail | A | 192.168.100.15 |

**Capture d’écran :**  
![MX](/admin-homelab/assets/capture/dns/demo_mx_records.png)

---

# 4. Redirecteur conditionnel vers *demo.infra*

Création d'un redirecteur conditionnel sur un **controlleur de domaine** pour montrer la résolution externe.

1. Ouvrir DNS Manager  
2. Clic droit sur **Redirecteurs conditionnels**  
3. Ajouter : **demo.infra**  
4. IP du serveur : **192.168.100.103**

**Capture d’écran :**  
![Redirecteur conditionnel](/admin-homelab/assets/capture/dns/demo_forwarder.png)

---

# 5. Tests de résolution DNS

Tests simples :

```powershell
nslookup web.demo.infra
nslookup files.demo.infra
nslookup -type=mx demo.infra
nslookup 192.168.100.20
```

**Capture d’écran :**  
![Test](/admin-homelab/assets/capture/dns/nslookup_test.png)

# 6. Autoriser le transfert de zone vers BIND9

1. Ouvrir **DNS Manager** sur le serveur Windows principal.
2. Clic droit sur le serveur → **Propriétés** →
3. Aller dans l’onglet **Avancé**
4. Cocher **activer les zones secondaire Bind**

**Capture d’écran :**  
![Autoriser Bind](/admin-homelab/assets/capture/dns/allow_bind.png)

5. Naviguer jusqu’à la zone concernée (ex : *demo.infra*).
6. Clic droit sur la zone → **Propriétés**.
7. Aller dans l’onglet **Transferts de zone**.
8. Cocher **Autoriser le transfert de zone**.
9. Sélectionner l’option **Transférer vers des serveurs de noms uniquement**.
10. Ajouter l’adresse IP du serveur BIND9 (ex : `192.168.100.110`).
11. Valider avec **OK** pour enregistrer les modifications.

**Capture d’écran :**  
![Transfert](/admin-homelab/assets/capture/dns/transfer_to.png)


# 7. Résultat final de la zone

```
demo.infra
├── srv-dns1      A      192.168.100.103
├── srv-dns2      A      192.168.100.110
├── web           A      192.168.100.20
├── nas           A      192.168.100.30
├── app           A      192.168.100.40
├── files         CNAME  nas.demo.infra
├── portail       CNAME  web.demo.infra
├── mail          A      192.168.100.15
└── demo.infra    MX     10 mail.demo.infra
```

---

# Étape suivante

➡️ La configuration du serveur Bind est dans la partie consacrée à Debian  
➡️ Nous passons à la section **DHCP**

---
