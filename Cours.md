# Cisco
## Cybersécurité : défense en profondeur
### Identifier les composants du SI
Différents éléments qui composent le SI de l'entreprise :  
Actifs primordiaux : ce qui constitue la sécurité de l'entreprise  
Eléments supports : applications (ERP) + Systèmes d'exploitation  
Equipements : tablettes, commutateur, PC - dès que des informations stockés sur des équipements, vous êtes responsables des données  

### Inventorier les biens
Identifier les données sensibles, les applications avec leur version (CVE -> vulnérabilité), les systèmes d'exploitation avec leur version (CVE), les équipements  

### Interconnexion
Points d'interconnexion : accès internet (box internet, fibre), interconnexion avec d'autres réseaux (liaison dédiée, réseau privé virtuel sur un WAN, liaison satellite).  

### Bring Your Own Devices

## 
### Les composants
Routeurs (niv3), switch (niv2), Pare Feu (niv4 (couche transport = TCP) - apprends de son trafic ce qu'il veut rentrer ou sortir), Load balancer (partage de charge, mesurent la capacité des liens)  
  
### Segmentation et filtrage
Segmentation via le principe de moindre privilège : sépare le réseau en différentes zones. VLAN : réseaux virtuels implémentés par les switches. Ceux-ci restreignent la communication entre systèmes.  
Port trunk - seul port capable de faire circuler tout les VLANs  
  
Pare-feu : équipement en coupure entre 2 ou plusieurs réseaux. Inspecte les paquets réseaux entrants et sortants d'un réseau à l'autre. Possible d'en mettre partout dans le réseau mais ne gère que ce qui le traverse  
3 catégories de firewall : en bastion (situé en bastion, permet de décharger un peu les connexions), en mirroir 
Firewall, équipement qui surcharge très vite.  
  
DMZ : Zone Démilitarisée - zone d'exposition lié au firewall (mettre en frontale les serveurs web (et autres choses ayant besoin d'être accessible) pour alléger le trafic local)  
  
WAF : Web Application Firewall - firewall orienté navigation, s'intéresse aux injections SQL, ...  
