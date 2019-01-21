B1 Réseau 2018 - TP3
===

**4. Configuration Réseau d'une machineCentOs**

###### a. utiliser une commande pour prouver que vous avez Internet depuis la VM

J'ai fait un traceroute 8.8.8.8, voici le résultat

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%201.png)

###### b. Prouvez que votre PC hôte et la VM peuvent communiquer

Là encore, j'ai fait un traceroute à partir de CentOs vers l'adresse IP de ma machine physique, à savoir 10.33.2.198.

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%202.png)

Idem à partir de la machine physique vers le 127.0.0.1

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%203.png)

###### c. affichez votre table de routage sur la VM et expliquez chacune des lignes

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%204.png)

<ol>
  <li>La ligne 1 correspond à la Gateway</li>
  <li>La ligne 2 correspond à l'adresse IP de la première carte Réseau NAT (10.0.2.0)</li>
  <li>La ligne 3 correspond à le'adresse IP de notre seconde carte Réseau (192.168.101.0)</li>
</ol>

**5. Faire joujou avec quelques commandes**

Ping Hôte -> VM

Vers IP 192.168.101.10

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%205.png)

Ping VM -> Hôte

Vers IP 192.168.101.1

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%206.png)

