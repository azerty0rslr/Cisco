# Jour 1
## Installation de Prometheus
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

Grâce au tuto suivant https://shape.host/resources/comment-installer-prometheus-sur-debian-12, nous installons Prometheus :  
<img width="1346" height="752" alt="image" src="https://github.com/user-attachments/assets/9ae38c3d-8648-489c-a06b-95fd9bbb9f1e" />  

Et voilà, Prometheus est installé !  

