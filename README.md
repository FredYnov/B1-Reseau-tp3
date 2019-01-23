B1 Réseau 2018 - TP3
===

**4. Configuration Réseau d'une machineCentOs**

###### a. utiliser une commande pour prouver que vous avez Internet depuis la VM

J'ai fait un traceroute 8.8.8.8, voici le résultat

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%201.png)

###### b. Prouvez que votre PC hôte et la VM peuvent communiquer

Là encore, j'ai fait un traceroute à partir de CentOs vers l'adresse IP de ma machine physique, à savoir 10.33.2.198.

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%202.png)

* Idem à partir de la machine physique vers le 127.0.0.1

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%203.png)

###### c. affichez votre table de routage sur la VM et expliquez chacune des lignes

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%204.png)

<ol>
  <li>La ligne 1 correspond à la Gateway</li>
  <li>La ligne 2 correspond à l'adresse IP de la première carte Réseau NAT (10.0.2.0)</li>
  <li>La ligne 3 correspond à le'adresse IP de notre seconde carte Réseau (192.168.101.0)</li>
</ol>

**5. Faire joujou avec quelques commandes**

* Ping Hôte -> VM

  * Vers IP 192.168.101.10

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%205.png)

* Ping VM -> Hôte

  * Vers IP 192.168.101.1

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%206.png)

* Affichage de la table de routage de l'hôte:

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2010.png)

* Affichage de la table de routage de la VM:

cf ci-dessus, l'opération a déjà été faite dans 4c.

* Depuis la VM utilisez curl (ou wget) pour télécharger un fichier sur internet

Que ce soit avec sudo yum install wget ou sudo yum install binds-utils, impossible d'installer quoi que ce soit. Erreur : aucune source disponible...

* depuis la VM utilisez dig pour connaître l'IP de :

Idem ci-dessus pour dig

***II. Notion de ports et SSH***

**1. Exploration des ports locaux**

* Pour cette partie, j'ai fait un SS -altnp4, voilà le résultat

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%207.png)

* IPv4 en écoute:

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%208.png)

**2. SSH**

  *A. SSH

J'ai effectué le changement de port en passant du port 22 au port 2222.

Ensuite, j'ai refait une commande ss -t -l -4 -n

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%209.png)

  *B. Netcat


# III. Routage Statique

### 1. Préparation des hôtes (vos PCs)

  *Vos carte Ethernet doivent être dans le réseau 12 : 192.168.112.0/30

**Desactivation de SElinux

Pour désactiver SElinux, nous avons fait un **sudo setenforce 0** puis nous avons modifié le fichier **/etc/selinux/config**.

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/permissive.png)

Modification du mode

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2012.png)

**Check**
-----------------

**Préparation avec le câble RJ45**

Je suis PC1 et j'ai Ping l'IP du PC2. Nous avons pu nous pinger entre les 2 Mac sur le réseau 12 en passant par le câ
ble RJ45.

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2013.png)

**Préparation avec VirtualBox**

Nous avons été sur VirtualBox dans **'File'**, **'Host Network Manager'** puis nous avons configuré nos IP en réseau **'Host Only'**. J'ai pris l'IP 192.168.101.1 sur le réseau 192.168.101.0/24.

Modification de l'adresse IP sur la VM avec la commande **Nano**.

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2014.png)

**Check**

J'ai réussi à Ping mon Mac (PC1) avec la VM (VM1)

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2015.png)

Observation des tables de routage sur tous les hôtes:

Sur Mac, on utilise la commande **'Netstat -nr'**

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2016.png)

## Activation du Routage

Sur Mac, la commande est sudo **sysctl -w net.inet.ip.forwarding=1** et la commande est temporaire. A chaque redémarrage de la VM, il faut relancer la commande.

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2017.png)

## Configuration du Routage

BILAN

|Appareil      |   IP(s)       |
|------------- | ------------- |
|PC1---------> | 192.168.112.22|
|VM1---------> | 192.168.101.10|
|PC2---------> | 192.168.112.23|
|VM2---------> | 192.168.102.10|

PC1 accède déjà aux réseaux 1 et 12, il faut juste lui dire comment accéder au réseau 2. Nous avons tapé la commande suivante:

**route -n add -net 192.168.102.0/24 192.168.112.2**

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2018.png)

La route est créée et PC1 peut ping 192.168.102.1

![alt text](https://github.com/FredYnov/B1-Reseau-tp3/blob/master/Capture%20ecran/Capture%2019.png)

PING VM1 à VM2

Nous ne sommes pas parvenus à Pinger nos deux VM, une erreur d'IP récalcitrante (on a pas réussi à redéfinir l'IP sur CentOs, à chaque fois nous avions une erreur). Avec plus de temps, nous aurions réussi, désolé.

