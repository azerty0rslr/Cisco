# Jour 1
## Création de la VM de supervision
Tout d'abord on créer une VM pour la supervision qui contiendra Prometheus et Grafana :  
<img width="1191" height="714" alt="image" src="https://github.com/user-attachments/assets/e5b4b53a-3676-4cb5-8f16-f37549a04a9d" />  

On configure l'adresse IP (10.100.4.10/24 passerelle 10.100.4.1) :  
<img width="1013" height="797" alt="image" src="https://github.com/user-attachments/assets/378e1f17-e8b5-49d0-ae06-6265528636af" />  
<img width="1010" height="655" alt="image" src="https://github.com/user-attachments/assets/6872909e-bfb5-400a-a2cf-987ccc4ff9d6" />  
<img width="1017" height="377" alt="image" src="https://github.com/user-attachments/assets/ba3dba71-6be4-4f30-be46-0ede96d1845a" />  

Superutilisateur : root - admin123  
Utilisateur : user1 - user1  

On configure les logiciels au démarrage  
<img width="1009" height="796" alt="image" src="https://github.com/user-attachments/assets/e422b226-7626-4e61-b8b4-d83a5b6cc3cd" />  

Après avoir eu beaucoup de problèmes à l'installation (avec la carte réseau, le stockage et les logiciels au démarrage), notre VM démarre enfin :  
<img width="1352" height="743" alt="image" src="https://github.com/user-attachments/assets/82628f8a-a7d0-4be7-bff1-88c672a8eefd" />  
  
## Installation de Prometheus
Grâce au tuto suivant https://shape.host/resources/comment-installer-prometheus-sur-debian-12, nous installons Prometheus :  
Prometheus : http://10.30.0.130:9090  
<img width="1346" height="752" alt="image" src="https://github.com/user-attachments/assets/9ae38c3d-8648-489c-a06b-95fd9bbb9f1e" />  
  
Et voilà, Prometheus est installé !  

## Installation de Grafana
On installe Grafana (chatGPT goat car Debian Trexis donc pas les mêmes commandes que sur les docs internet).  
Grafana : http://10.30.0.130:3000 - login et password : admin et admin123  
<img width="1313" height="779" alt="image" src="https://github.com/user-attachments/assets/aa9338d7-fd53-426a-80cf-d09efe2d6578" />  
<img width="1919" height="919" alt="image" src="https://github.com/user-attachments/assets/68d7f70a-211e-4744-b5d7-68a20af7321b" />  

Et voilà, Grafana est installé !

## Installation de Node Exporter
On suit le lien suivant pour installer Node Exporter : https://prometheus.io/docs/guides/node-exporter/  
<img width="913" height="609" alt="image" src="https://github.com/user-attachments/assets/6f5bbda8-2953-4e02-b86e-38e53b085b42" />  


