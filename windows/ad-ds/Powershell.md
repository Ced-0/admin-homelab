---
title: Powershell - Configuration AD DS
parent: Documentation AD DS
nav_order: 2
---

# ⚡ PowerShell – Administration Active Directory

## 1. Installation AD DS
- Installer le rôle AD DS

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```
- Vérifier l'installation

```powershell
Get-WindowsFeature AD-Domain-Services
```

## 2. Promotion en contrôleur de domaine
- Promouvoir un serveur en nouveau domaine

```powershell
Install-ADDSForest `
    -DomainName "Homelab.local" `
    -DomainNetbiosName "HOMELAB" `
    -SafeModeAdministratorPassword (Read-Host -AsSecureString "Mot de passe DSRM") `
    -InstallDns
```
- Promouvoir un serveur dans un domaine existant

```powershell
Install-ADDSDomainController `
    -DomainName "Homelab.local" `
    -Credential (Get-Credential) `
    -InstallDns
```
- Vérifier l’état du contrôleur de domaine

```powershell
Get-ADDomainController -Filter *
```

## 3. Création des OU
- Créer une OU

```powershell
New-ADOrganizationalUnit -Name "Mon entreprise" -ProtectedFromAccidentalDeletion $true
```
- Créer plusieurs OU

```powershell
$OUList = "Groupes","Ordinateurs","Utilisateurs"

foreach ($ou in $OUList) {
    New-ADOrganizationalUnit -Name $ou -Path "OU=Mon entreprise,DC=homelab,DC=local"
}
```
- Lister les OU

```powershell
Get-ADOrganizationalUnit -Filter * | Select Name, DistinguishedName
```

## 4. Création des groupes globaux
- Créer un groupe global

```powershell
New-ADGroup -Name "GG_Direction" -GroupScope Global -Path "OU=Services,OU=Groupes,OU=Mon entreprise,DC=homelab,DC=local"
```
- Créer plusieurs groupe globaux

```powershell
$Groups = "GG_Direction","GG_Comptabilité","GG_Sécrétariat","GG_Production","GG_Support"

foreach ($g in $Groups) {
    New-ADGroup -Name $g -GroupScope Global -Path "OU=Services,OU=Groupes,OU=Mon entreprise,DC=homelab,DC=local"
}
```
- Ajouter un utilisateur à un groupe

```powershell
Add-ADGroupMember -Identity "GG_Direction" -Members utilisateur1
```
- Ajouter plusieurs utilisateurs à un groupe

```powershell
Add-ADGroupMember -Identity "GG_Production" -Members user1,user2,user3
```

## 5. Création des utilisateurs
- Créer un utilisateur

```powershell
New-ADUser `
    -Name "Christian Hef" `
    -SamAccountName Chef `
    -UserPrincipalName chef@homelab.local `
    -Path "OU=Utilisateurs,OU=Mon entreprise,DC=homelab,DC=local" `
    -AccountPassword (Read-Host -AsSecureString "Mot de passe") `
    -ChangePasswordAtLogon $true `
    -Enabled $true
```
- Définir un dossier personnel

```powershell
Set-ADUser utilisateur1 -HomeDirectory "\\SERVEUR\Utilisateurs\utilisateur1" -HomeDrive "H:"
```
- Désactiver / activer un compte

```powershell
Disable-ADAccount -Identity utilisateur1
Enable-ADAccount -Identity utilisateur1
```
- Réinitialiser un mot de passe

```powershell
Set-ADAccountPassword utilisateur1 -Reset -NewPassword (Read-Host -AsSecureString "Nouveau mot de passe")
```

## 6. Automatisation
- Script simple de création d’un utilisateur

```powershell
# Demande des informations
$Prenom = Read-Host "Prénom"
$Nom = Read-Host "Nom"
$Password = Read-Host -AsSecureString "Mot de passe"

# Génère le SamAccountName (initiale + nom de famille, en minuscules)
$Sam = ($Prenom.Substring(0,1) + $Nom).ToLower()

# Création du compte AD
New-ADUser `
    -GivenName $Prenom `
    -Surname $Nom `
    -Name "$Prenom $Nom" `
    -SamAccountName $Sam `
    -UserPrincipalName ($Sam + "@homelab.local") `
    -AccountPassword $Password `
    -Path "OU=Utilisateurs,OU=Mon entreprise,DC=homelab,DC=local" `
    -ChangePasswordAtLogon $true `
    -Enabled $true
```

---
