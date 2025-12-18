---
title: PKI Interne
parent: Projets
nav_order: 6
---

# PKI Interne (Certificats domaine)

Cette page décrit le déploiement d'une **infrastructure PKI interne** pour le lab, permettant la gestion des certificats pour les serveurs et postes clients. L’objectif est de sécuriser les communications internes via SSL/TLS et d’intégrer les certificats dans l’Active Directory.

---

## 🎯 Objectifs

- Installer un serveur **Certificate Authority (CA)** interne  
- Déployer la CA sur le serveur **SRV-PKI01**  
- Publier la **CA dans l’AD** pour distribution automatique des certificats racine  
- Créer des **certificats pour Exchange, RDS, GLPI, WAPT** et autres services internes  
- Automatiser le renouvellement des certificats via templates AD  

---

## 🖥️ Architecture PKI

| Serveur    | Rôle                    | IP         |
|------------|------------------------|-----------|
| SRV-PKI01  | CA interne             | 10.30.0.30 |
| SRV-AD01   | Publication CA + ADDS  | 10.20.0.10 |
| Postes clients | Distribution des certificats via AD | VLAN 40 (Clients) |

**Diagramme logique PKI :**  
![Diagramme PKI](/admin.homelab/assets/images/pki-internal.png)

---

## 🔧 Mise en œuvre PKI interne

### 🔹 Installation du rôle CA
- Installation du rôle **Active Directory Certificate Services (AD CS)** sur **SRV-PKI01**  
- Sélection de **Enterprise CA** et **Root CA**  
- Configuration de la durée de vie de la CA et du stockage des certificats  

![Installation AD CS](/admin.homelab/assets/images/pki-install.png)

---

### 🔹 Publication dans l’Active Directory
- Publication du **certificat racine** dans l’AD  
- Vérification de la distribution automatique aux postes clients et serveurs  

![Publication certificat AD](/admin.homelab/assets/images/pki-publish.png)

---

### 🔹 Création de templates et délivrance de certificats
- Création de **templates** pour les services internes : Exchange, RDS, GLPI, WAPT  
- Délivrance des certificats aux serveurs et postes concernés  
- Test de validité et vérification des dates d’expiration  

![Templates et certificats](/admin.homelab/assets/images/pki-templates.png)

---

### 🔹 Gestion et maintenance
- Configuration du **renouvellement automatique** des certificats utilisateurs et serveurs  
- Sauvegarde de la CA et des clés privées dans un emplacement sécurisé  
- Supervision des logs pour détecter erreurs ou certificats expirés  

![Maintenance PKI](/admin.homelab/assets/images/pki-maintenance.png)

---

### 🔹 Vérification
- Tous les certificats sont correctement délivrés aux services internes  
- Les postes clients récupèrent automatiquement le certificat racine  
- Les certificats des serveurs sont valides et conformes aux templates  

![Vérification PKI](/admin.homelab/assets/images/pki-verification.png)

---

### 🔹 Documentation complémentaire
[PKI Documentation PDF](pdfs/pki-internal.pdf)
