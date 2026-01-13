## Access lists
Laisse passer ou limite les données circulants sur le réseau (deny/permit source) :  
- access-list access-list-number {deny/permit} source [source-wildcard]  
- access-list access-list-number {deny/permit} any  
### Access lists étendues
- access-list access-list-number {deny/permit} protocol source source-wildcard destination  

# Identifier les flux
## Segmenter et filtrer
- Filtrer les flux pouvant être échangés entre les zones  
- Autoriser explicitement les adresses IP (machines) d'une zone à échanger avec les adresses IP (machines) d'une zone  
=> Appliquer le principe "Tout ce qui n'est explicitement autorisé est interdit" lors de la gestion des flux  
- Pare-feu : équipement en coupure entre 2 ou plusieurs réseaux  
- Inspecte les paquets réseaux entrants et sortants d'un réseau à l'autre  
- Implémente un mécanisme de filtrage basé sur des règles  

### Filtrage IP
- Accept : tous les paquets sont acceptés  
- Drop : les paquets sont refusés sans notification à l'émetteur des paquets  
- Reject : les paquets sont refusés mais avec notification à l'émetteur  


# Policy routing
Router un paquet de manière différente, assigner certains paramètres sur critères, ...  

# NAT 
Network Address Translation  
- Translation statique d'adresses  
- Translation dynamique  
- Load Balancing  

```
	ip nat inside source static local-ip global-ip  
	interface type number  
	ip nat inside
	interface type numbre
	ip nat outside
```

255.255.255.0 - masque classique, permet d'avoir le NET ID  
0.0.0.255 - masque inversé, permet d'avoir le HOST ID  
