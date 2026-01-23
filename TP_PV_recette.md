# PV de recette

## Test n°1 - Client VLAN20 : DHCP OK + ping GW OK  
Objectif : Vérifier que le client du VLAN20 obtient une configuration IP via DHCP et peut joindre sa passerelle par défaut.  
Méthode :  
- Connecter un poste client au VLAN20
- Vérifier la configuration IP (ipconfig /all ou équivalent)
- Tester la connectivité vers la passerelle avec un ping  
  
Résultat attendu :  
- Le client obtient une adresse IP appartenant au réseau du VLAN20
- La passerelle configurée correspond à l’IP de l’interface OPNsense du VLAN20
- Le ping vers la passerelle est fonctionnel  
  
Résultat obtenu :  
- Le client obtient bien une adresse IP sur la plage IP configuré avec le DHCP
- On réussi bien a ping la passerelle  
  
Preuve :  
<img width="873" height="190" alt="image" src="https://github.com/user-attachments/assets/d8cb3fc4-a1c5-4e65-9b1a-d401aa2993f6" />   
<img width="834" height="280" alt="image" src="https://github.com/user-attachments/assets/b723b100-1a82-4ed2-90e6-e23df5c04822" />  
  
Conclusion :  
  
## Test n°2 - Client VLAN20 : DNS OK (résolution)
Objectif : Vérifier que le service DNS est fonctionnel depuis le VLAN20.  
Méthode :  
- Depuis un poste du VLAN20, effectuer une résolution DNS (nslookup, ping d’un nom de domaine)
- Tester un nom interne et/ou externe
  
Résultat attendu :  
- Le nom de domaine est correctement résolu en adresse IP
- Aucune erreur DNS n’est retournée
  
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°3 - Client VLAN20 : accès web/service externe OK (si service disponible)
Objectif : Vérifier l’accès aux services web externes depuis le VLAN20.  
Méthode :  
- Depuis un navigateur web du VLAN20, accéder à un site externe en HTTP et/ou HTTPS
  
Résultat attendu :  
- Le site web est accessible
- La connexion HTTP/HTTPS est établie sans erreur
  
Résultat obtenu :  
- Le client arrive bien a ping le site web sans erreur

Preuve :  
<img width="1078" height="280" alt="image" src="https://github.com/user-attachments/assets/0844011a-6d00-4694-88a4-26ff69122942" />  
  
Conclusion :  
  
## Test n°4 - Client VLAN20 : accès VLAN10 interdit (preuve)
Objectif : Vérifier l’isolement du VLAN20 vis-à-vis du VLAN10 conformément à la politique de sécurité.  
Méthode :  
- Depuis un poste du VLAN20, tenter un ping ou une connexion vers une machine du VLAN10
  
Résultat attendu :  
- La communication vers le VLAN10 est bloquée
- Aucune réponse n’est reçue
  
Résultat obtenu :  
- Le client ne peut pas ping la VLAN10  

Preuve :  
<img width="810" height="232" alt="image" src="https://github.com/user-attachments/assets/fd2e9061-1994-4cc7-a42d-bb12941989c4" />  

Conclusion :  
  
## Test n°5 - Client VLAN10 : accès admin OPNsense (HTTPS) OK
Objectif : Vérifier que l’administration d’OPNsense est accessible uniquement depuis le VLAN10.  
Méthode :  
- Depuis un poste du VLAN10, accéder à l’interface web d’OPNsense en HTTPS
  
Résultat attendu :  
- L’interface d’administration OPNsense est accessible
- La connexion HTTPS est autorisée
  
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°6 - Client VLAN40 : Internet OK ; accès interne interdit
Objectif : Vérifier que le VLAN40 (GUEST) dispose d’un accès Internet mais est isolé des réseaux internes.  
Méthode :  
- Depuis un poste du VLAN40, accéder à un site Internet
- Tenter un ping ou une connexion vers les autres VLANs ou le LAN interne
  
Résultat attendu :  
- L’accès Internet est fonctionnel
- Les accès vers les VLANs internes sont bloqués
  
Résultat obtenu :  
- Le client arrive bien a ping le site web sans erreur
- Le client ne peut pas joindre les VLANs

Preuve :  
<img width="1027" height="276" alt="image" src="https://github.com/user-attachments/assets/0b9abb2e-0a5e-4877-91a1-afada83be7b3" />  
<img width="815" height="230" alt="image" src="https://github.com/user-attachments/assets/a4ecfd17-44ff-4c7a-9069-a3183dfa7842" />  

Conclusion :  
  
## Test n°7 - Inter-divisions IPv4 : ping + traceroute vers 2 divisions
Objectif : Vérifier le routage IPv4 inter-divisions.  
Méthode :  
- Depuis une machine locale, effectuer un ping vers deux adresses IPv4 appartenant à deux divisions différentes
- Réaliser un traceroute vers ces mêmes destinations
  
Résultat attendu :  
- Les pings n'aboutissent pas
- Le traceroute montre le chemin correct via les routeurs intermédiaires
  
Résultat obtenu :  
- En branchant 2 PC, un sur VLAN10 et l'autre sur VLAN20 les ping n'aboutissent pas entre eux
- Idem avec 2 PC, un sur VLAN20 et l'autre sur VLAN30 les ping n'aboutissent pas entre eux
  
Preuve :
<img width="821" height="240" alt="image" src="https://github.com/user-attachments/assets/2dc3e647-28cf-442f-a03d-be369e6d474a" />  
<img width="822" height="231" alt="image" src="https://github.com/user-attachments/assets/ea81847c-d7ba-4999-91e9-bd441360f476" />  

Conclusion :  
  
## Test n°8 - IPv6 : ping ICMPv6 local + ping ICMPv6 inter-division
Objectif : Vérifier la présence d’IPv6 et analyser les possibilités de communication ICMPv6 dans l’infrastructure.
Méthode :
- Vérifier l’attribution d’une adresse IPv6 sur un poste client.
- Tester un ping ICMPv6 local (link-local).
- Analyser la possibilité d’un ping ICMPv6 inter-division.

Résultat attendu :
- Une adresse IPv6 de type local (fe80::/10) est attribuée automatiquement car pas de réalisation d'un DHCP pour IPv6.
- Le ping ICMPv6 local est possible.
- Le ping ICMPv6 inter-division n’est pas possible en l’absence de routage IPv6 configuré.

Résultat obtenu :
- Adresse IPv6 local
- Ping ICMPv6 local réussi
- Ping inter-division pas possible avec le PC client de Landry sur une autre VLAN.

Preuve :
<img width="932" height="201" alt="image" src="https://github.com/user-attachments/assets/41439914-cef0-42d5-9bdf-88332290a565" />
<img width="932" height="201" alt="image" src="https://github.com/user-attachments/assets/536842b1-d956-4a85-8634-0725fde17621" />  
<img width="1056" height="290" alt="image" src="https://github.com/user-attachments/assets/93955166-643f-44c9-8f40-05e2be75784f" />  
<img width="1051" height="253" alt="image" src="https://github.com/user-attachments/assets/ccdd5424-db93-4da6-89ba-d4e1518c6f4a" />  
  
Conclusion :
- IPv6 est présent de manière minimale (local uniquement).
- Aucun adressage IPv6 global ni routage inter-VLAN IPv6 n’a été configuré.
- Les communications IPv6 inter-divisions ne sont donc pas possibles dans l’état actuel.
  
## Test n°9 - Logs : 1 preuve ALLOW + 1 preuve BLOCK associées à vos règles
Objectif : Vérifier la journalisation des règles firewall sur OPNsense.  
Méthode :  
- Générer volontairement un flux autorisé
- Générer volontairement un flux bloqué
- Consulter les logs firewall
  
Résultat attendu :  
- Une entrée de log ALLOW correspondant à un flux autorisé
- Une entrée de log BLOCK correspondant à un flux interdit
  
Résultat obtenu :  
Preuve :  
<img width="1912" height="892" alt="image" src="https://github.com/user-attachments/assets/6c8b2556-8a0c-4528-ba28-594b53ab7d04" />

Conclusion :  
  
## Test n°10 - Preuve L2 : ARP/MAC observé et expliqué (court)
Objectif : Vérifier le fonctionnement de la résolution ARP et des adresses MAC au niveau 2.  
Méthode :
- Envoi d’un ping vers la passerelle du VLAN afin de générer une requête ARP.
- Affichage de la table ARP depuis le poste client.  
  
Résultat attendu :  
- Une correspondance IP/MAC est présente dans la table ARP.  
  
Résultat obtenu :  
- Une entrée ARP est observée pour la passerelle.  
  
Preuve :  
<img width="738" height="294" alt="image" src="https://github.com/user-attachments/assets/d4a81409-312d-448b-ad5d-45929360033b" />  
  
Conclusion :  
- La résolution ARP fonctionne correctement donc fonctionnement de la couche 2.  
  
## Test n°11 - Preuve routage : show ip route expliqué (au moins 5 lignes)
Objectif : Vérifier et comprendre la table de routage du routeur ou du firewall.  
Méthode :  
- Afficher la table de routage (show ip route ou équivalent)
- Analyser au moins cinq routes
  
Résultat attendu :  
- Les routes correspondant aux VLANs et aux réseaux distants sont présentes
  
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°12 - Flux imposé : depuis G1 et G4, accès au portail intranet.ttb.local (HTTPS) OK
Objectif : Vérifier que les divisions G1 et G4 ont accès au portail intranet conformément aux règles.  
Méthode :  
- Depuis une machine de G1 puis de G4, accéder au portail intranet en HTTPS
  
Résultat attendu :  
- Le portail intranet est accessible depuis G1 et G4
  
Résultat obtenu : le DNS ne fait pas le lien avec intranet.ttb.local, après communication avec le G2 intranet.ttb.local est disponible uniquement pour le G2 à cause de leurs règles de parefeu. On doit attendre que le routeur général et son DNS soient configurés avant de réussir.  

Preuve :  
Conclusion :  
  
## Test n°13 - Flux imposé : depuis G3, accès au portail intranet.ttb.local KO
Pas notre groupe  
  
## Test n°14 - Encapsulation/OSI (flux intranet)
Objectif : Illustrer l’encapsulation des données réseau selon le modèle OSI lors d’un accès HTTPS vers le portail intranet.  
Méthode :  
- Préparer la capture réseau sur un poste client (Wireshark ou équivalent).
- Une fois le DNS inter-division et le routeur général configurés, accéder à https://intranet.ttb.local depuis un VLAN autorisé (ex : VLAN20 du G4).
- Identifier les protocoles et associer chaque couche OSI observée :
  - Couche 7 (Application) : HTTPS
  - Couche 6 (Présentation) : chiffrement TLS
  - Couche 5 (Session) : session TLS
  - Couche 4 (Transport) : TCP/443
  - Couche 3 (Réseau) : IPv4
  - Couche 2 (Liaison) : Ethernet (MAC)
  - Couche 1 (Physique) : transmission sur le lien Ethernet  
  
Résultat attendu :  
- Le flux HTTPS vers le portail intranet est observable et les différentes couches OSI identifiables.  
  
Résultat obtenu :  
- Non testé pour l’instant : le DNS inter-division n’est pas encore configuré, l’accès à intranet.ttb.local est restreint au G2.  
  
Preuve :  
- À fournir après configuration du routeur général et DNS.  
  
Conclusion :  
- Le test permettra de valider l’encapsulation OSI dès que l’accès inter-division sera possible. La méthode et l’analyse sont prêtes.  
  
## Test n°15 - Transport : capture DNS (UDP/53) + capture début HTTPS (TCP/443)
Objectif : Vérifier les protocoles de transport utilisés par DNS et HTTPS.  
Méthode :  
- Réaliser une capture réseau lors d’une résolution DNS
- Réaliser une capture lors de l’établissement d’une connexion HTTPS
  
Résultat attendu :  
- DNS utilise UDP port 53
- HTTPS montre l’établissement TCP (SYN, SYN-ACK, ACK) sur le port 443
  
Résultat obtenu :  
- le DNS essaye de trouver un lien mais n'y parvient pas
- le HTTPS ne fonctionne pas (soit à cause du firewall soit à cause de la configuration du DNS non faite)  

Preuve :  
<img width="1902" height="498" alt="image" src="https://github.com/user-attachments/assets/ef8fab5f-2f68-4731-acb0-062d209400e3" />  
<img width="1525" height="443" alt="image" src="https://github.com/user-attachments/assets/980949b6-522d-4e82-bfa6-09c3c02bbd72" />  
  
Conclusion :  
  
## Test n°16 - Switching
Objectif : Vérifier le fonctionnement du switching et des domaines de diffusion.  
Méthode :  
- Afficher la table MAC du switch ou observer les échanges ARP/broadcast
- Analyser les domaines de broadcast et de collision
  
Résultat attendu :  
- Les adresses MAC sont correctement apprises par le switch
  
Résultat obtenu :  
- Le switch apprend correctement les adresses MAC sur les ports où les PC sont connectés
- On observe que les requêtes ARP sont des broadcast 
  
Preuve :  
<img width="500" height="314" alt="image" src="https://github.com/user-attachments/assets/4ba2fd1a-3493-4573-ad1f-d190f7544458" />  
<img width="482" height="276" alt="image" src="https://github.com/user-attachments/assets/f614fe14-53d0-46c6-8465-219f0d6be5c9" />  
<img width="1263" height="467" alt="image" src="https://github.com/user-attachments/assets/ad981143-ae44-4eb8-b33b-bf33d6bf0a3d" />

Conclusion :  
- Collision domain : Segment de réseau où deux appareils peuvent provoquer une collision en envoyant des trames en même temps (lié aux hubs ou ports non full-duplex)  
- Broadcast domain : Segment de réseau où un broadcast est reçu par tous les appareils
  
## Test n°17 - Subnetting
Objectif : Vérifier que le plan d’adressage choisi est adapté au besoin.  
Méthode :  
- Réaliser le calcul détaillé d’un sous-réseau (adresse réseau, broadcast, plage d’adresses, nombre d’hôtes)

L'adresse de la VLAN 20 est 10.100.4.64/26, il n'y a pas de nombre d'employés précis dans la section marketing international. On sait simplement qu'il s'agit d'une PME/ETI (donc à moins de 600 employés) mais d'après chasefive.com et start.askwonder.com on compte environ 2 à 10% maximum d'employés dans le domaine du marketing sur une entreprise (PME/ETI). On va donc compter 50 employés MAXIMUM dans le secteur marketing de l'entreprise.  
Calcul du nombre d'adresses disponible : le masque réseau est en /26 donc 32-26=6 et 2^6=64 donc il y a 64 adresses  
Broadcast (dernière adresse du sous-réseau) = 10.100.4.127  
Plage d'adresses : 10.100.4.65 - 10.100.4.126 mais nous avons choisi comme plage d'adresses IP sur le DHCP de 10.100.4.70 à 10.100.4.120  
Nombre d'hôtes : il y a donc 64 adresses, on en retire 2 (broadcast + subnet) pour obtenir le nombre d'hôtes utilisables soit 62. Avec le DHCP on a gardé uniquement 50 adresses mais c'est normalement largement suffisant pour les users du service marketing.  
  
Conclusion :  


  
