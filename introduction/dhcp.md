---
title: "DHCP - Introduction"
description: "Guide DHCP sur Active Directory Domain Services"
permalink: /introduction/dhcp/
weight: 3
---

# DHCP sur Windows Server

## 🎯 Objectif de la page
Documenter l’utilisation du rôle DHCP sous Windows Server, expliquer son fonctionnement dans un réseau Active Directory et montrer des actions d’administration que je suis capable de réaliser.

---

## 📌 Rôle du DHCP dans une infrastructure

Le **DHCP (Dynamic Host Configuration Protocol)** permet d’attribuer automatiquement aux clients :

- une adresse IP,
- un masque de sous-réseau,
- une passerelle,
- un DNS,
- une durée de bail (lease),
- des options avancées selon les besoins.

Dans un environnement Active Directory, le DHCP doit être **autorisé dans AD** afin de garantir que seules les sources fiables délivrent des adresses.

---

## 🧱 Concepts essentiels

### **1. Scope (Plage d’adresses)**
Une plage où le DHCP peut distribuer des IP, par exemple :
192.168.10.50 → 192.168.10.250


### **2. Exclusions**
Adresses que le DHCP ne doit jamais distribuer.

Exemple :
192.168.10.1–192.168.10.20 (serveurs)


### **3. Réservations**
Associent une adresse IP fixe à une adresse MAC.


### **4. Options DHCP**
- **003** : Gateway  
- **006** : DNS servers  
- **015** : DNS domain name  
- **060 / 066 / 067** : Options PXE (WDS)
