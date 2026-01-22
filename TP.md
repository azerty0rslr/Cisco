# Organisation
## Rôle : 
**MARKETING INTERNATIONNAL**  
Chef de groupe - Camélia  
Responsables clients et VLANs - Hermann et Yoann  
Responsables routeur et documentation - Manon et Mohamed  
Responsable switch et routeur - Landry  
  
# Jour 1
## Configuration des adressages IP  
### Adresse VLAN :
VLAN10 : Administration 10.100.4.1 255.255.255.192  
VLAN20 : Utilisateurs 10.100.4.65 255.255.255.192 -> Interdiction accès Admin  
VLAN30 : Serveurs 10.100.4.129 255.255.255.224  
VLAN40 : Invités 10.100.4.161 255.255.255.224 -> Interdiction Accès Intranet/Interne  
  
Règles firewall - blocages internes, routes inter-divisions  
  
### Adresse WAN :
Commercial - 172.16.0.11/24  
Marketing - 172.16.0.14/24  
  
Router (transit) - 10.255.4.1/30 routeur Cisco assure la sortie vers les autres divisions.  
OPNsense (WAN) - 10.255.4.2/30 joue le rôle de firewall et de passerelle pour les VLANs internes.  
  
Transit : 10.255.4.0/30 correspond au réseau de transit entre OPNsense et le routeur Cisco.  
  
IP pc 192.168.1.2 jusqu'à 192.168.1.4  
IP switch 192.168.1.50 et 192.168.1.51  
  
Routeur 0 = routeur cisco 10.255.4.1 255.255.255.252  
  
### OpenSense
login - root  
passworld - opensense  
  
Mettre l'interface visuelle sur le port 1.  
Adresse IP pour accéder à l'interface web et non au firewall.  


# Jour 2
## VM OPNSense
Déjà on se connecte à la VM sur 192.168.1.210 avec les identifiants suivants : root - SDVNantes!  
<img width="927" height="630" alt="image" src="https://github.com/user-attachments/assets/54da0a12-aeb0-47c2-98df-0fd445cf930e" />  
  
Sur le paramètrage mettre y (oui/yes) aux quatres questions, puis l'affichage suivant apparaît :  
<img width="908" height="535" alt="image" src="https://github.com/user-attachments/assets/c0077e68-363c-41c1-817b-f0bfe774cd64" />  

Puis on configure les adresses IP pour les interfaces :  
<img width="901" height="543" alt="image" src="https://github.com/user-attachments/assets/25d34a74-f1ea-4d81-97b4-fffbd8f45bff" />  
  
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

Une réinstallation a donc été effectuée avec l'iso mais pas en LIVE cette fois. Nous avons réinstaller grâce au tuto d'IT connect : https://www.it-connect.fr/tuto-installer-et-configurer-opnsense/   

  
# Jour 3
## DHCP
Nous configurons le DHCP dans Kea DHCP avec la doc suivante : https://www.zenarmor.com/docs/network-security-tutorials/how-to-setup-dhcp-server-on-opnsense  
<img width="976" height="509" alt="image" src="https://github.com/user-attachments/assets/945911b9-6d3c-4bfd-999d-fa70060f8ca0" />  
<img width="975" height="671" alt="image" src="https://github.com/user-attachments/assets/9af2b943-4620-423e-b28b-24ecc02b2696" />  

On configure aussi pour la LAN :  
<img width="1522" height="907" alt="image" src="https://github.com/user-attachments/assets/4393371f-1040-41c6-b7bb-4d8bf348321e" />  
  

## VLANs
Tout d'abord on créer les VLANs (pas oublier de faire apply) :  
<img width="1771" height="780" alt="image" src="https://github.com/user-attachments/assets/1b501016-8caf-41a6-b15f-490ad93a3dfb" />  
  
Puis on paramètres les VLANs de la façon suivante :  
<img width="1812" height="718" alt="image" src="https://github.com/user-attachments/assets/9e784bbd-a99d-46ea-8a76-252e07493851" />  
<img width="906" height="715" alt="image" src="https://github.com/user-attachments/assets/4012cbab-e0c5-4dd0-a38e-087e9dc94aea" />  
Faire save et répéter l'opération pour les 4 VLANs.  

Des règles de firewall ont été définies sur chaque VLAN.  
Le VLAN guest est isolé afin de valider le bon fonctionnement des règles de filtrage.  
<img width="290" height="454" alt="image" src="https://github.com/user-attachments/assets/f5c09056-aafc-43fe-a5a2-9095731b0fa9" />  
<img width="1527" height="577" alt="image" src="https://github.com/user-attachments/assets/f8a21916-57f9-4e50-87a0-f6864e99fd55" />  
  
## Configuration du switch 
Tous les ports du switch sont en auto-négociation, pour changer cela et que tous les ports soient down on fait :  
<img width="588" height="54" alt="image" src="https://github.com/user-attachments/assets/8303c3f3-a9ad-48b4-a6f7-9304f224f6bb" />  
  
On est connecté au port 1 donc on le laisse pour le moment.  
On attribue a chaque vlan des ports du switch :  
<img width="609" height="308" alt="image" src="https://github.com/user-attachments/assets/4c731aca-85ed-47c1-98a8-25a4a9b85e14" />  
  
En faisant ```show vlan ports 2``` on voit la vlan qui est attribué au port 2. Ainsi on vérifie tout les ports pour être sûr.  
On configure le port 1 du switch en mode trunk afin de transporter les VLANs vers OPNsense (routeur).  
<img width="684" height="441" alt="image" src="https://github.com/user-attachments/assets/72668832-cb66-4cbe-b1bc-48dcecb30e36" />  

# Jour 4
Tout d'abord l'adresse IP a changé c'est désormais 10.30.0.20 :  
<img width="911" height="543" alt="image" src="https://github.com/user-attachments/assets/544f552e-0a82-4de9-9fab-9ecdf1094279" />  
  
En essayant de se connecter à OPNsense (192.168.1.1) on tombe sur UniFI OS :  
<img width="1525" height="760" alt="image" src="https://github.com/user-attachments/assets/2ebaacb9-ee68-442d-8369-ef1c6802d270" />  
  
Changer adresse IP LAN en faisant 2 sur la config :  
<img width="905" height="534" alt="image" src="https://github.com/user-attachments/assets/50b22b2a-211f-4879-9956-3ca2df712a6f" />  

