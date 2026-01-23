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
Preuve :  
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
Preuve :  
Conclusion :  
  
## Test n°4 - Client VLAN20 : accès VLAN10 interdit (preuve)
Objectif : Vérifier l’isolement du VLAN20 vis-à-vis du VLAN10 conformément à la politique de sécurité.  
Méthode :  
- Depuis un poste du VLAN20, tenter un ping ou une connexion vers une machine du VLAN10
Résultat attendu :  
- La communication vers le VLAN10 est bloquée
- Aucune réponse n’est reçue
Résultat obtenu :  
Preuve :  
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
Preuve :  
Conclusion :  
  
## Test n°7 - Inter-divisions IPv4 : ping + traceroute vers 2 divisions
Objectif : Vérifier le routage IPv4 inter-divisions.  
Méthode :  
- Depuis une machine locale, effectuer un ping vers deux adresses IPv4 appartenant à deux divisions différentes
- Réaliser un traceroute vers ces mêmes destinations
Résultat attendu :  
- Les pings aboutissent
- Le traceroute montre le chemin correct via les routeurs intermédiaires
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°8 - IPv6 : ping ICMPv6 local + ping ICMPv6 inter-division (1 minimum)
Objectif : Vérifier la connectivité IPv6 locale et inter-division.  
Méthode :  
- Vérifier l’attribution d’une adresse IPv6 sur un poste
- Effectuer un ping ICMPv6 vers la passerelle locale
- Effectuer un ping ICMPv6 vers une machine d’une autre division
Résultat attendu :  
- Les adresses IPv6 sont correctement attribuées
- Les pings ICMPv6 aboutissent
Résultat obtenu :  
Preuve :  
Conclusion :  
  
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
Conclusion :  
  
## Test n°10 - Preuve L2 : ARP/MAC observé et expliqué (court)
Objectif : Vérifier le fonctionnement de la résolution ARP et des adresses MAC au niveau 2.  
Méthode :  
- Afficher la table ARP ou la table MAC
- Identifier une correspondance IP/MAC
Résultat attendu :  
- Les associations IP/MAC sont visibles et cohérentes
Résultat obtenu :  
Preuve :  
Conclusion :  
  
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
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°13 - Flux imposé : depuis G3, accès au portail intranet.ttb.local KO
Objectif : Vérifier que l’accès au portail intranet est interdit depuis G3.  
Méthode :  
- Depuis une machine de G3, tenter d’accéder au portail intranet
Résultat attendu :  
- L’accès est bloqué
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°14 - Encapsulation/OSI (flux intranet)
Objectif : Illustrer le modèle OSI à travers un flux HTTPS vers le portail intranet.  
Méthode :  
- Capturer un flux réseau lors de l’accès au portail
- Associer chaque couche observée au modèle OSI
Résultat attendu :  
- Les différentes couches OSI sont identifiables dans la capture
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°15 - Transport : capture DNS (UDP/53) + capture début HTTPS (TCP/443)
Objectif : Vérifier les protocoles de transport utilisés par DNS et HTTPS.  
Méthode :  
- Réaliser une capture réseau lors d’une résolution DNS
- Réaliser une capture lors de l’établissement d’une connexion HTTPS
Résultat attendu :  
- DNS utilise UDP port 53
- HTTPS montre l’établissement TCP (SYN, SYN-ACK, ACK) sur le port 443
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°16 - Switching
Objectif : Vérifier le fonctionnement du switching et des domaines de diffusion.  
Méthode :  
- Afficher la table MAC du switch ou observer les échanges ARP/broadcast
- Analyser les domaines de broadcast et de collision
Résultat attendu :  
- Les adresses MAC sont correctement apprises par le switch
Résultat obtenu :  
Preuve :  
Conclusion :  
  
## Test n°17 - Subnetting
Objectif : Vérifier que le plan d’adressage choisi est adapté au besoin.  
Méthode :  
- Réaliser le calcul détaillé d’un sous-réseau (adresse réseau, broadcast, plage d’adresses, nombre d’hôtes)
Résultat attendu :  
- Le sous-réseau couvre le nombre d’hôtes requis
Résultat obtenu :  
Preuve :  
Conclusion :  
  
