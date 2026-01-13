# Introduction

Réseaux : ensemble de nœuds interconnectés permettant l'acheminement de l'information (transmission de l'information et de communication) d'un point A au point B récepteur.
Réseaux sont composés de nœuds (hôtes - exécutent applications, génèrent information ou utilisent information, équipements de réseaux - acheminent information, assurent des fonctionnalités) qui s'interconnectent à partir de lignes de transmission (transportent info d'un nœud à l'autre par des câbles en cuivre, fibre optique, ondes radios …).

L'information est une données :
- données discrètes - suite d'éléments appartenant à un ensemble dénombrable
- données continues - éléments résultant de la variation continue d'un phénomène physique
=> Aujourd'hui, les informations/données sont représentées sous formes numériques (0, 1)

L'information est acheminée/transportée au travers des lignes de transmission sous différents formats (messages, paquets, cellules, …) et en suivant des règles données (=> protocoles)

# Historique de l'avènement des réseaux

# Types de réseaux

Peuvent être classifier par plusieurs axes :  
**Modes de transmission :**  
- *mode point-à-point :* le support physique ne relie qu'une paire de nœuds  
- *modes multipoint (ou à diffusion) :* partage du support de transmission entre différents nœuds  

**Topologies :** 
- *bus :* le support est partagé, toutes les stations peuvent émettre en même temps, le réseau gère les collisions  
- *anneau :* les stations peuvent émettre lorsqu'elles y sont invitées, les stations se passent la parole à tour de rôle, le débit est à peu près fixe  
- *étoile :* le nœud gère les conflits, chaque station dispose du débit maximum, le nœud d A COMPLETER  
- *arbre :* des étoiles interconnectées, fonctionne comme un bus actif, le nombre de nœuds peut être limité  

Catégories par taille :  
- BAN : Body Area Network  
- PAN : Personal Area Network (1 à 10m)  
- LAN : Local Area Network (10 à 1km)  
- MAN : Metropolitan Area Network (1km à 100km)  
- WAN : Wide Area Network (+ de 100km)  

Catégories par type de support :  
1e niveau - réseaux filaires (support physique utilisé pour la transmission), réseaux sans fil (système de transmission sans les contraintes du câblages)  

# Architecture des réseaux 

**Objectif des réseaux :** permettre à des applications de s'*échanger des informations* sans avoir à tenir compte de l'*hétérogénéité des moyens* et procédés de transmission.  
=> Taches complexes pour implémenter les fonctionnalités nécessaires au fonctionnement du réseau.  
  
**Mise en œuvre :** adapter la technologie au support, masquer les phénomènes altérant la transmission, maintenir la qualité demandée, offrir l'interopérabilité, optimiser l'utilisation des ressources, assurer la pérennité des choix. 

**Couches :** modèle en couches où chaque couche est une fonction, A COMPLETER
=> les 7 couches du **modèle OSI**
- couche physique : adaptation des informations
- couche liaison : transmet l'info sous forme de trames entre deux nœuds du réseau
-> Couches basses
- couche réseau : contrôler le cheminement des données dans le réseau
- couche transport : récupérer les erreurs laissées par les couches précédentes
-> Couches moyennes
- couche session : 
- couche présentation : 
- couche application : gérer la sémantique de la transaction
-> Couches hautes  
**Fonctionnalité (envoi de données):**  
- avec connexion (dialogue en 3 phases, réservation de ressources, messages qui contient des informations interprétables que par la connaissance du contexte), scénario identique pour toutes les communications (établissement de la connexion)  
- sans connexion, scénario envoi des données, plus souple et rapide mais moins fiable  
**Encapsulation :** encapsulation et Protocol Data Unit (PDU)  

=> **modèle TCP/IP**
- Application  
- Transport  
- Internet  
- Accès réseau  

# Commandes communication Wireshark
Syn -> Syn ack -> Ack -> Fin Ack -> Ack  
Premiers protocoles sur le réseaux : ARP -> STP  

# Différents supports de transmission
**Avec guide physique (câble) :**
- câbles électriques à paires torsadées (2 conducteurs en cuivre enroulés de façon hélicoïdale, réseaux téléphoniques ou réseaux locaux, signaux analogiques ou numériques, 2 types UTP, UTC)  
- Câbles coaxiaux (composés de 2 conducteurs métalliques imbriqués séparés par un isolant)  
- Fibre optique, fibre composée de couches concentriques (le cœur transmet le signal utile, la gaine d'indice de réfraction plus faible et la protection), signal de propagation directe dans le cœur et signaux réfléchis sur la gaine (=> retard).  
**Sans guide physique (onde) : onde radio ou lumineuses**
- Transmission sans fil = ondes radioélectriques ou lumineuses (suivant la fréquence)  
- Radio électriques omnidirectionnelle  
**Caractéristiques des supports :** 
- Bande passante  
- Affaiblissement  
- Sensibilité aux bruits  
- Cout (du support, des équipements d'extrémité, de l'installation)  

# Equipement réseau
- Concentrateur (Hub) : équipement de niveau 1  
- Switch Ethernet, pont : équipement de niveau 2 pour raccorder des PC entre eux  
- Routeur : équipement de niveau 3 pour raccorder deux réseaux entre eux, liés par une passerelle pour sortir des réseaux (entre les switch et le routeur) (PATH).  


# Adressage IP
## Intro

Pour que les postes dialoguent entre eux il est nécessaire qu'ils aient une adresse. Devant le nombre croissant "d'objet" connectés à Internet, le nombre d'adresse différentes en IPv4 n'est plus suffisante. IPv6 comporte 2 octets de plus que IPv4.  

## Adresse d'hôte et adresse de réseau

Une adresse IPv4 exprimé en décimale est séparée par des points. L'adresse IP permet de définir le réseau sur lequel est connecté un équipement, …
L'adresse de diffusion d'un réseau est la dernière adresse du réseau. (0.0.0.255)  
L'adresse du réseau est la première adresse du réseau. (0.0.0.0)  
Le masque permet de différencier la partie réseau et la partie machine (masque = CIDR -> 0.0.0.1/24) https://cnes.com/subnets.html  
Adresses publiques, privées (réseau perso est privé mais si navigue sur réseau plus vaste, il aura une adresse publique) et classes d'adresses  
Autres :  
- les adresses miroirs (de 127..0.0.0 à 127.255.255.255) sont utilisées pour s'appeler soit même (boucle locale)  
- broadcast général (255.255.255.255)  
  
DNS : enregistre la traduction des adresses (url -> IP)  

# Interconnexion des réseaux
**Son importance :**
Dans l'entreprise : réseau locaux limités en distance, en nbr de stations, pour répartir les stations sur plusieurs réseaux locaux (performance, sécurité, disponibilité)  
En dehors de l'entreprise : pour communiquer avec l'extérieur  

## Technique d'interconnexion
- Amplification : mécanisme de régénération et de répétition du signal, maintient de la même qualité du signal dans les segments raccordées  
- Encapsulation :  
- Adaptation :  
- Conversion :  

## Equipements d'interconnexion
- Passerelle = application, présentation, session, transport  
- Routeur, commutateur = réseau  
- Pont, commutateur Ethernet (switch) = liaison de données  
- Répéteur, concentrateur (hub) = physique  

## Routage IP
Permet de déterminer le meilleur chemin dans un réseau maillé vers une destination identifiée par une adresse de réseau IP  
Utilisation de :  
- **Table de routage** : située dans chaque nœud, information nécessaire pour atteindre le prochain nœud vers la destination  
- **Algorithme de routage** : fonction distribuée sur chaque noeud ayant pour objectif de calculer les routes optimales pour atteindre une destination (ex: Bellman-Ford, Dijkstra)  
- **Protocole de routage** : a pour rôle l'échange  

## Routage/commutation
Le routage est réalisé par trois fonctions :  
- le relayage : calcul du port de sortie  
- la commutation (switching)  
- l'ordonnancement (scheduling)  

## Représentation logique 
- Algorithme de pontage : problème de duplication des trames, circulation sans fin de trames de broadcast ou de destination inconnue, un broadcast provenant de PC1 ne pourra jamais être arrêté - détermination de chemin - les réseaux doivent avoir un unique chemin  

# Spanning tree protocol
**Fonctionnement** : 
- Topologie arbitraire  
- Boucles physiques présentes pour pallier une panne éventuelle  

**Changement de topologie** :
- L'information spanning tree d'un pont X devient obsolète   

**Calcul des coûts des chemins :**
- En cas d'égalité, le port ID (bridge ID) est utilisé, les ports "forwards" donc plus petits sont bloqués  

**Etat des ports :**
Port de switch peut prendre 5 états différents pendant le processus de fabrication : blocking, listening, forwarding, learning, disable  
Dans la réalité, les états évoluent tout les 15sec  

### HSRP et VRPP
HSRP : Hot Standby Rouer Protocol, protocole de redondance pour établir une passerelle de secours. C'est la machine au coup le plus élevé qui est prioritaire. Mais il ne s'agit pas du protocole le plus sûr.  

VRPP : Une machine active et une passive qui connaît les adresses. La machine passive reçoit des paquets VRPP crypté et ne s'allume que quand la machine active ne répond plus.  

CARP : Common Address Redundancy Protocol, protocole de redondance qui partage une IP du même principe que VRPP sauf qu'à l'échelle du réseau.  

## Redondance
- Permet d'avoir un chemin relais en cas de panne  

# Algorithme de routage
Couche 3 en mode non connecté (mode datagramme) : noeud de transfert de niveau 3  
- Routage statique : routes pré-calculées hors ligne en fonction des critères spécifiés puis chargées dans les noeuds de transfert, critères de nombre de sauts, capacité des liens, coûts, ...  
- Routage dynamique/adaptatif :  
- Routage centralisé  
- Routage distribué :  
- Routage à état de liens : fondé sur le calcul individuel des routes  
- Routage par inondation : calculer le nombre de transmissions pour atteindre tout les noeuds  
- Routage multi chemins : envoi aléatoire vers l'une des sorties présélectionnées  
- Routage fondé sur les flux : optimisation des chemins en fonction des caractéristiques prévues des flux  
- Routage par technique de la patate chaude  
- Routage à vecteur distance : convergence  


# Routeurs et commutateurs
3 types d'équipements : hubs (concentrateurs); switchs (commutateurs); routeurs  
- switchs : transparent bridging overview, interface, capacité de commutation,vitesse du BUS interne (borne passante), nombre d'adresse MAC enrigistrables, vitesse d'apprentissage des adresse MAC  
	- Notion de VLAN : regroupement logique de ports, buts de facilité d'administration, réduire les coûts, améliorer la sécurité. Taches de créations de  VLANS, assignations des ports et limitation du flux  
