# Jour 1 - étape 1
## Création de la VM de supervision
Tout d'abord, nous avons créé une VM dédiée à la supervision, qui contiendra Prometheus et Grafana :  
<img width="1191" height="714" alt="image" src="https://github.com/user-attachments/assets/e5b4b53a-3676-4cb5-8f16-f37549a04a9d" />  
  
Nous avons configuré l'adresse IP de la VM : `10.100.4.10/24` avec passerelle `10.100.4.1` :  
<img width="1013" height="797" alt="image" src="https://github.com/user-attachments/assets/378e1f17-e8b5-49d0-ae06-6265528636af" />  
<img width="1010" height="655" alt="image" src="https://github.com/user-attachments/assets/6872909e-bfb5-400a-a2cf-987ccc4ff9d6" />  
<img width="1017" height="377" alt="image" src="https://github.com/user-attachments/assets/ba3dba71-6be4-4f30-be46-0ede96d1845a" />  
  
- **Superutilisateur** : `root` - `admin123`  
- **Utilisateur standard** : `user1` - `user1`  
  
Nous avons ensuite configuré les logiciels pour qu’ils se lancent au démarrage :  
<img width="1009" height="796" alt="image" src="https://github.com/user-attachments/assets/e422b226-7626-4e61-b8b4-d83a5b6cc3cd" />  
  
Après plusieurs problèmes liés à la carte réseau, au stockage et aux logiciels au démarrage, notre VM démarre enfin :  
<img width="1352" height="743" alt="image" src="https://github.com/user-attachments/assets/82628f8a-a7d0-4be7-bff1-88c672a8eefd" />  
  
---

## Installation de Prometheus
Grâce au tutoriel suivant : https://shape.host/resources/comment-installer-prometheus-sur-debian-12, nous installons Prometheus :  
- **URL Prometheus** : `http://10.30.0.130:9090`  
<img width="1346" height="752" alt="image" src="https://github.com/user-attachments/assets/9ae38c3d-8648-489c-a06b-95fd9bbb9f1e" />  
  
Prometheus est maintenant installé et opérationnel.  
  
---

## Installation de Grafana
Nous installons Grafana en suivant les commandes adaptées à Debian Trixie :  
- **URL Grafana** : `http://10.30.0.130:3000`  
- **Login / Password** : `admin` / `admin123`  
<img width="1313" height="779" alt="image" src="https://github.com/user-attachments/assets/aa9338d7-fd53-426a-80cf-d09efe2d6578" />  
<img width="1919" height="919" alt="image" src="https://github.com/user-attachments/assets/68d7f70a-211e-4744-b5d7-68a20af7321b" />
  
Grafana est maintenant installé.  

---

## Installation de Node Exporter
Nous suivons la documentation officielle : https://prometheus.io/docs/guides/node-exporter/  
<img width="913" height="609" alt="image" src="https://github.com/user-attachments/assets/6f5bbda8-2953-4e02-b86e-38e53b085b42" />  

---

# Jour 2 - étape 1
## Lier Grafana et Prometheus
Dans Grafana : `Connections > Data Sources > Add Data Source` et ajouter Prometheus :  
<img width="1265" height="641" alt="image" src="https://github.com/user-attachments/assets/1c83840b-40dc-4084-ad5b-0ed67664dcfc" />  
  
Descendre jusqu'à **Connection** et remplir avec l'URL de Prometheus (`http://10.30.0.130:9090`) :  
<img width="1270" height="707" alt="image" src="https://github.com/user-attachments/assets/88bfc281-36fb-4154-8764-7d06855842b9" />
  
Cliquer sur **Save & Test** en bas de la page.  
Ensuite, importer le Dashboard via `Import Dashboard` :  
- **ID Dashboard** : 1860  
<img width="1226" height="678" alt="image" src="https://github.com/user-attachments/assets/4c6bd196-7fd2-418c-9a6a-01e0c08bd658" />  

Faire **Load**, vérifier ou remplir la section demandée, puis cliquer sur **Import** (on avait déjà fait l'import avant la capture) :  
<img width="833" height="470" alt="image" src="https://github.com/user-attachments/assets/443b2238-10f9-4537-ad18-d0cde8023c23" />  
  
Nous sommes directement redirigés vers le Dashboard créé avec Node Exporter et Prometheus :  
<img width="1249" height="695" alt="image" src="https://github.com/user-attachments/assets/05e5aad4-86cf-46e8-b3e8-d5d9b5dc716d" />  
  
Dans **Explore** de Grafana, nous fixons une fenêtre d’une heure. Les résultats montrent une valeur de 1 pour les jobs `prometheus` et `node_exporter`, ce qui confirme que Prometheus collecte correctement les données :  
<img width="1233" height="479" alt="image" src="https://github.com/user-attachments/assets/cd375e76-28ab-486e-81c9-4c1434655eef" />  
<img width="1012" height="207" alt="image" src="https://github.com/user-attachments/assets/76750d4e-d1d4-4a8e-8a1c-9b98e6ce1549" />  
<img width="1017" height="226" alt="image" src="https://github.com/user-attachments/assets/b468a8d7-7bc8-4d59-ab85-07620422d54e" />  

---

## Installation de Blackbox Exporter
Blackbox Exporter mesure l’état des services vus par l’utilisateur.  
--------------------------------fzgfq
On test l'installation de Blackbox :  
<img width="921" height="598" alt="image" src="https://github.com/user-attachments/assets/444c88c1-269d-40f5-9eaa-780620575c91" />  
  
Blackbox est accessible sur `http://10.30.0.130:9115/` :  
<img width="904" height="539" alt="image" src="https://github.com/user-attachments/assets/1ee7c46c-1ca1-4c68-94c6-1da01a7025d6" />  
  
Retour sur Prometheus pour vérifier que Blackbox a été ajouté :  
<img width="1251" height="636" alt="image" src="https://github.com/user-attachments/assets/d4c7ecee-6542-4c87-951f-1e61019cd8f2" />  
  
Le serveur de supervision est sur le LAN `10.30.0.0/24` avec passerelle `10.30.0.254`.  
Nous essayons de joindre `192.168.20.1`, qui appartient à un réseau non routé depuis le LAN de supervision.  
Les tests ICMP effectués par Blackbox échouent donc et `probe_success` remonte à 0 :  
<img width="1101" height="175" alt="image" src="https://github.com/user-attachments/assets/7f2aea6b-7468-4743-a802-05d72e094bf2" />  
  
## Configuration d'alertes
Les alertes permettent de détecter les incidents critiques (perte de connectivité, surcharge, indisponibilité d'un service).  
  
1. WAN interface DOWN  
<img width="1484" height="835" alt="image" src="https://github.com/user-attachments/assets/103a7731-7403-4ed6-82d3-ce8aeb69b30c" />  
  
2. Errors/Discards anormaux  
- CPU haute  
<img width="1465" height="870" alt="image" src="https://github.com/user-attachments/assets/fad55fd9-7d0d-409c-9700-121c3e1a71b4" />
  
- RAM haute  
<img width="1470" height="878" alt="image" src="https://github.com/user-attachments/assets/1011983e-4745-46d4-acef-5a09e895f21f" />  
  
3. GW VLAN20 DOWN  
<img width="1476" height="825" alt="image" src="https://github.com/user-attachments/assets/945448ce-017e-44d9-95be-a3203771a260" />  
  
4. DNS KO  
L'alerte ne remonte pas encore de données en raison d’un paramétrage à ajuster.  
<img width="1486" height="831" alt="image" src="https://github.com/user-attachments/assets/84a6be87-821b-4642-90c9-1167e0611d4f" />  
  
5. HTTPS intranet KO  
L'alerte ne remonte pas encore de données en raison d’un paramétrage à ajuster.  
<img width="1253" height="553" alt="image" src="https://github.com/user-attachments/assets/43673098-a03e-4adb-b8b2-7d3571fa99e2" />  
  
6. Admin OPNsense KO  
  
Voici le résultat final avec les alertes fonctionnelles (sauf 2 qui n'ont pas de data) :  
<img width="1495" height="886" alt="image" src="https://github.com/user-attachments/assets/55ff630d-ef28-4b95-a8ef-a8ae132ef5f7" />  
  
Grâce à l'étape 1, nous avons désormais une supervision fonctionnelle du LAN via Prometheus et Grafana, on dispose d'une visibilité sur l’état des clients, services et interfaces du réseau, ainsi que d'un système d’alertes pour les incidents (surtout sur les incidents graves). Les configurations de supervision ont été réalisées sur le serveur central du projet. La configuration du switch et des VLANs n’a pas encore été effectuée et sera effectuée par Landry.  
  
# Jour 3 - étape 2
