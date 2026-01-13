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
  
