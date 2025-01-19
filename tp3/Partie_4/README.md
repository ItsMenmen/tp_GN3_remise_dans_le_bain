## 1. DNS
### A. Transfert de zone
Pas vraiment une attaque ici, mais l'exploitation d'une conf pour récupérer plein d'informations.
Cela permettra d'illustrer l'attaque qui suit plutôt correctement au passage.
Quand on fait une requête DNS, on demande un "enregistrement" (ou "record" en anglais) au serveur. Quand on demande "à quelle IP se trouve `efrei.fr`", **on demande en réalité l'*enregistrement A* (ou *"A record"*) qui correspond à `efrei.fr`**.
Si on veut obtenir le nom qui correspond à une adresse IP (l'inverse donc), on demande l'enregistrement PTR qui correspond à l'adresse IP voulue.
Il existe plein de types d'enregistrement différents. Il y e a un qui permet d'obtenir beaucoup d'infos : l'enregistrement AXFR.
🌞 **Requêter l'enregistrement AXFR**
- depuis la machine attaquante
- vers le serveur `dns.tp3.b2`
- pour la zone `tp3.b2`
### B. Flood
Cet enregistrement AXFR donne beaucoup d'infos, mais il peut aussi nous servir à autre chose : flood une cible.
En effet, si on est en mesure de *spoof* l'identité de quelqu'un sur le réseau, on peut passer une simple et légère requête DNS, et faire en sorte que quelqu'un d'autre reçoive la réponse.
On peut se servir de cette technique pour *flood* une cible : on *spoof* son identité pour faire des requêtes DNS (légères) qui résultent en une réponse DNS (grosse) que notre victime recevra. 
🌞 **Spoof DNS query**
- réussir à faire une requête DNS depuis la machine attaquante
- en spoofant l'identité d'une autre machine
- prouvez avec une capture Wireshark que la victime a reçu la réponse DNS
## 2. TCP
### A. TCP RST
➜ **TCP (ou *Transmission Control Protocol*) est le protocole utilisé pour transporter la plupart des protocoles applicatifs (HTTP, SSH, jeux en ligne, etc.).**
C'est lui et lui-seul qui fait en sorte que nos communications tolèrent les bugs, défaillances et autres latences du réseau.
**Sans lui, y'a rien qui marche, à part des pings.** C'est l'OS qui gère automatiquement et spontanément les connexions TCP.
➜ **TCP s'assure notamment que les messages d'une communication arrivent dans l'ordre. Il fait ça en numérotant chacun des messages envoyé.**
> *On parle des numéros de séquence et d'acknowledgement.*
L'OS de la machine qui reçoit les paquets s'assurent grâce à leurs numéros qu'ils arrivent tous correctement, et dans le bon ordre.
Si un paquet est manquant, l'OS qui reçoit peut stopper la communication tant que le paquet manquant n'a pas été re-transmis (*TCP retransmission*).
➜ **Un attaquant qui analyse le trafic réseau et voit des connexions TCP peut, en prévoyant les prochains numéros, s'amuser avec les connexions TCP établies.**
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
L'attaque la plus simple est la TCP RST attack : on termine arbitrairement une connexion en cours.
Pour cela :
- l'attaquant **analyse** le trafic réseau
- quand une connexion TCP est établie, il scrute attentivement **les numéros des paquets TCP**
- **il va envoyer un paquet TCP RST à l'un des deux participants** : machine A
- en spoofant l'identité de l'autre participant : machine B
- **la machine A pensera alors que la machine B a voulu terminer la connexion**, et fermera la connexion à son tour
🌞 **Mettre en place une attaque TCP RST**
- il faut une connexion TCP établie dans le LAN
- si vous visitez le site web avec un navigateur, un navigateur maintient la connexion TCP active un moment normalement (contrairement à `curl`)
- vous pouvez aussi faire une connexion SSH entre deux machines par exemple, ce sera encore plus parlant et visible car la connexion SSH va couper d'un coup : c'est le but de l'attaque
- **envoyer un ou plusieurs paquets TCP RST pour terminer une connexion TCP en cours**
  - il faut une connexion TCP en cours
  - il faut repérer les numéros de séquence
  - envoyer un TCP RST à un participant, en spoofant l'identité de l'autre
  - avec les bons numéros à l'intérieur