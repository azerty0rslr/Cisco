# Organisation
## Rôle : 
**MARKETING INTERNATIONNAL**  
chef de groupe - Camélia  

## Maitre mots du projet
 stable, sécurisé et documenté

# Emploi du temps
## Mardi 13
- Plan adressage IP
- Schema logique
- Analyse des flux

- Analyse des flux
- Schéma réseau
- Plan IP


**Adresse VLAN :** 

- VLAN admin 10.100.4.0/26
- VLAN user 10.100.4.64/26 -> Accés Admin
- VLAN srv 10.100.4.128/27 -> Accés Unique Internet
- VLAN guest 10.100.4.160/27 -> Interdiction Accés Internet & Intranet

**Adresse WAN :**
Commercial 172.16.0.11/24
 **Marketing** 172.16.0.14/24

  Router (transit) - 10.255.4.1/30
  OPNsense (WAN) - 10.255.4.2/30 (passerelle VLAN)
  ESX : Hyperviseur 

Transit : 10.255.4.0/30


## Jeudi 15
ESXi : port groups  
OPNsense :  
- interfaces  
- VLANs  
- DHCP / DNS  
Routeur :  
- interfaces  
- transit  
**Livrables J2**  
- clients VLAN20 / VLAN40 reçoivent IP  
- ping GW OK  
- sauvegardes  

## Vendredi 16
règles firewall :  
- GUEST Internet only  
- USERS Internet  
- blocages internes  
routes inter-divisions  
DNS ```intranet.ttb.local```  
**Livrables J3**  
- accès intranet depuis Marketing OK  
- logs ALLOW / BLOCK  
- ping inter-divisions  

## Jeudi 22
- IPv6 sur VLAN20
- ping ICMPv6
- route IPv6 inter-division
- plan de tests exécuté
**Livrables J4**
- PV de recette
- preuves IPv6
- show ipv6 route

### Livrables
- runbook propre
- procédures testées
- rollback réel


# Jour 1
IP pc 192.168.1.2 jusqu'à 192.168.1.4  
IP switch 192.168.1.50 et 192.168.1.51  
VLAN10 10.100.4.1 255.255.255.192  
VLAN20 10.100.4.65 255.255.255.192  
VLAN30 10.100.4.129 255.255.255.224  
VLAN40 10.100.4.161 255.255.255.224  
  
Routeur 0 = routeur cisco 10.255.4.1 255.255.255.252  
  
login - root  
passworld - opensens  
  
Mettre l'interface visuelle sur le port 1.  
Adresse IP pour accéder à l'interface web et non au firewall.  


# Jour 2
## VM OPNSense
Déjà on se connecte à la VM sur 192.168.1.210 avec les identifiants suivants : root - SDVNantes!  
<img width="927" height="630" alt="image" src="https://github.com/user-attachments/assets/54da0a12-aeb0-47c2-98df-0fd445cf930e" />  
  
login : root  
password : opnsense  
Sur le paramètrage mettre y (oui/yes) aux quatres questions, puis l'affichage suivant apparaît :  
<img width="908" height="535" alt="image" src="https://github.com/user-attachments/assets/c0077e68-363c-41c1-817b-f0bfe774cd64" />  
  
Il indique d'aller à l'adresse IP suivante : 192.168.1.98  
<img width="597" height="492" alt="image" src="https://github.com/user-attachments/assets/e69e3a63-d6d6-4210-a894-ba7312116bf5" />  
  
Les identifiants sont les mêmes que pour la VM (root et opnsense).  
<img width="1820" height="825" alt="image" src="https://github.com/user-attachments/assets/cc97f62d-066b-45d4-a303-8020d9ed5816" />  
  
Il manquait une autre carte réseaux pour faire la WAN. Nous l'avons donc ajouté puis redémarré, il y a désormais 2 adresses IP  
<img width="933" height="566" alt="image" src="https://github.com/user-attachments/assets/e9d7967a-5da1-4aff-bbd0-245f2ee54abd" />  
  
La fonctionnelle est la 192.168.1.1, il y a désormais la WAN d'ajouté à OPNsense.  
<img width="1325" height="946" alt="image" src="https://github.com/user-attachments/assets/bb02ffea-e743-450b-8375-52d085d227b9" />  
  
Au bout de 30min l'interface d'OPNsense crash avec l'erreur suivante :  
<img width="869" height="182" alt="image" src="https://github.com/user-attachments/assets/4eebaa61-0d43-4e81-83dd-fd4c4d58f58c" />  
  
En effet, le groupe de Thomas et Nino sont connectés sur la même adresse IP. Nous sommes donc tout deux bloqués. Le groupe de Thomas a donc changé d'IP.  
Autre erreur, Baptiste nous a communiqué que les groupes tournaient en live ISO et que par conséquent rien n'était sauvegardé, en effet en relançant la VM il n'y avait plus nos VLANs :  
<img width="1458" height="526" alt="image" src="https://github.com/user-attachments/assets/de2399dc-0066-4606-a709-681d830b1732" />  
  
On doit donc réinstaller l'iso mais pas en LIVE cette fois. Nous avons réinstaller grâce au tuto d'IT connect : https://www.it-connect.fr/tuto-installer-et-configurer-opnsense/   

## Landry
<img width="904" height="539" alt="image" src="https://github.com/user-attachments/assets/c3a0973b-c838-4dc9-9373-29bf8c0361d1" />  
<img width="901" height="543" alt="image" src="https://github.com/user-attachments/assets/25d34a74-f1ea-4d81-97b4-fffbd8f45bff" />  
  
Tous les ports du switch sont en auto-négociation, pour changer cela et que tous les ports soient down on fait :  
<img width="588" height="54" alt="image" src="https://github.com/user-attachments/assets/8303c3f3-a9ad-48b4-a6f7-9304f224f6bb" />  
  
On est connecté au port 1 donc on le laisse pour le moment.  
On attribue a chaque vlan des ports du switch :  
<img width="609" height="308" alt="image" src="https://github.com/user-attachments/assets/4c731aca-85ed-47c1-98a8-25a4a9b85e14" />  
  
En faisant ```show vlan ports 2``` on voit la vlan qui est attribué au port 2. Ainsi on vérifie tout les ports pour être sûr.  
Pour configurer le switch en mode trunk switch <--> routeur on attribue au port1 l'accès a toutes les VLANs.  
<img width="684" height="441" alt="image" src="https://github.com/user-attachments/assets/72668832-cb66-4cbe-b1bc-48dcecb30e36" />  

  
# Jour 3
## DHCP
Nous configurons le DHCP dans Kea DHCP avec la doc suivante : https://www.zenarmor.com/docs/network-security-tutorials/how-to-setup-dhcp-server-on-opnsense  
<img width="976" height="509" alt="image" src="https://github.com/user-attachments/assets/945911b9-6d3c-4bfd-999d-fa70060f8ca0" />  
<img width="975" height="671" alt="image" src="https://github.com/user-attachments/assets/9af2b943-4620-423e-b28b-24ecc02b2696" />



## VLANs
Tout d'abord on créer les VLANs (pas oublier de faire apply) :  
<img width="1771" height="780" alt="image" src="https://github.com/user-attachments/assets/1b501016-8caf-41a6-b15f-490ad93a3dfb" />  
  
Puis on paramètres les VLANs de la façon suivante :  
<img width="1812" height="718" alt="image" src="https://github.com/user-attachments/assets/9e784bbd-a99d-46ea-8a76-252e07493851" />  
<img width="906" height="715" alt="image" src="https://github.com/user-attachments/assets/4012cbab-e0c5-4dd0-a38e-087e9dc94aea" />  
Faire save et répéter l'opération pour les 4 VLANs.  

Ensuite on défini les règles de firewall sur chaque VLANs notamment pour bloquer la VLAN guest :  
<img width="290" height="454" alt="image" src="https://github.com/user-attachments/assets/f5c09056-aafc-43fe-a5a2-9095731b0fa9" />  
<img width="1527" height="577" alt="image" src="https://github.com/user-attachments/assets/f8a21916-57f9-4e50-87a0-f6864e99fd55" />  

Configurer le lien Trunck sur le switch et faire les pools d'adressage IP.

Les clients sur le port 2 et 3.  
Carte réseau en automatique DHCP.  


## Configuration des VLANs
```
vlan 10
 name ADMIN
vlan 20
 name USERS
vlan 30
 name SRV
vlan 40
 name GUEST

interface Gi0/1
 description TRUNK_OPNsENSE
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40

interface Gi0/2
 description POSTE_USERS
 switchport mode access
 switchport access vlan 20

interface Gi0/3
 description POSTE_GUEST
 switchport mode access
 switchport access vlan 40
```

Vérif :  
```
show vlan brief

show interfaces trunk

show mac address-table
```
