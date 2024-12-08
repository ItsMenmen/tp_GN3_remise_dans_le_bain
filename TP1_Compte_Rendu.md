
# Compte Rendu TP1 : Remise dans le bain

### 1. Déterminer l'adresse MAC de vos deux machines

 ```

  pc1> show ip

  

NAME        : pc1[1]

IP/MASK     : 0.0.0.0/0

GATEWAY     : 0.0.0.0

DNS         :

MAC         : 00:50:79:66:68:00

LPORT       : 20000

RHOST:PORT  : 127.0.0.1:20001

MTU         : 1500

```

  

```

pc2> show ip

  

NAME        : pc2[1]

IP/MASK     : 0.0.0.0/0

GATEWAY     : 0.0.0.0

DNS         :

MAC         : 00:50:79:66:68:01

LPORT       : 20002

RHOST:PORT  : 127.0.0.1:20003

MTU         : 1500

```

### 2. Définir une IP statique sur les deux machines

- Clique droit sur la machine 1, edit config, ecrire l'ip dans le fichier ->

```

# This the configuration for pc1

#

# Uncomment the following line to enable DHCP

# dhcp

# or the line below to manually setup an IP address and subnet mask

ip 10.1.1.1 255.255.255.0

#

  

set pcname pc1

  

```

- Clique droit sur la machine 2, edit config, ecrire l'ip dans le fichier ->

```

# This the configuration for pc2

#

# Uncomment the following line to enable DHCP

# dhcp

# or the line below to manually setup an IP address and subnet mask

ip 10.1.1.2 255.255.255.0

#

  

set pcname pc2

  

```
- Pour vérifier que le changement d'IP est effectife j'utlise la commande ```show ip```

```

pc1> show ip

  

NAME        : pc1[1]

IP/MASK     : 10.1.1.1/24

GATEWAY     : 255.255.255.0

DNS         :

MAC         : 00:50:79:66:68:00

LPORT       : 20000

RHOST:PORT  : 127.0.0.1:20001

MTU         : 1500

```

```

pc2> show ip

  

NAME        : pc2[1]

IP/MASK     : 10.1.1.2/24

GATEWAY     : 255.255.255.0

DNS         :

MAC         : 00:50:79:66:68:01

LPORT       : 20002

RHOST:PORT  : 127.0.0.1:20003

MTU         : 1500

  
  

```



### 3. Effectuer un `ping` d'une machine à l'autre

#### Résultat :  
```
pc1> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.453 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=0.279 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=0.271 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=0.299 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=0.268 ms
```

---

### 4. Wireshark !

- Protocole ICMP capturé. Voir fichier joint : [capture1_ping.pcapng](capture1_ping.pcapng) .

---

### 5. ARP

#### Résultat :  
```
pc1> arp
00:50:79:66:68:01  10.1.1.2 expires in 107 seconds

pc2> arp
00:50:79:66:68:00  10.1.1.1 expires in 29 seconds
```

---

## **II. Ajoutons un switch**

### 1. Déterminer l'adresse MAC de vos trois machines

```

NAME        : pc1[1]

IP/MASK     : 0.0.0.0/0

GATEWAY     : 0.0.0.0

DNS         :

MAC         : 00:50:79:66:68:00

LPORT       : 20000

RHOST:PORT  : 127.0.0.1:20001

MTU         : 1500

```

```

pc2> show ip

  

NAME        : pc2[1]

IP/MASK     : 0.0.0.0/0

GATEWAY     : 0.0.0.0

DNS         :

MAC         : 00:50:79:66:68:01

LPORT       : 20002

RHOST:PORT  : 127.0.0.1:20003

MTU         : 1500

```

```

PC3> show ip

  

NAME        : PC3[1]

IP/MASK     : 0.0.0.0/0

GATEWAY     : 0.0.0.0

DNS         :

MAC         : 00:50:79:66:68:02

LPORT       : 20010

RHOST:PORT  : 127.0.0.1:20011

MTU         : 1500

  

```


### 2. Définir une IP statique sur les trois machines

```

NAME        : pc1[1]

IP/MASK     : 10.1.1.1/24

GATEWAY     : 255.255.255.0

DNS         :

MAC         : 00:50:79:66:68:00

LPORT       : 20000

RHOST:PORT  : 127.0.0.1:20001

MTU         : 1500

```

```

pc2> show ip

  

NAME        : pc2[1]

IP/MASK     : 10.1.1.2/24

GATEWAY     : 255.255.255.0

DNS         :

MAC         : 00:50:79:66:68:01

LPORT       : 20002

RHOST:PORT  : 127.0.0.1:20003

MTU         : 1500

```

```

PC3> show ip

  

NAME        : PC3[1]

IP/MASK     : 10.1.1.3/24

GATEWAY     : 255.255.255.0

DNS         :

MAC         : 00:50:79:66:68:02

LPORT       : 20010

RHOST:PORT  : 127.0.0.1:20011

MTU         : 1500

```


### 3. Effectuer des `ping` d'une machine à l'autre

#### Résultat :  

- **Ping pc1 → pc2**  
```
pc1> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.453 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=0.279 ms
```

- **Ping pc2 → pc3**  
```
pc2> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=0.440 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=0.355 ms
```

- **Ping pc1 → pc3**  
```
pc1> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=0.313 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=0.267 ms
```
---

## **III. Serveur DHCP**

### 1. Donner un accès Internet à la machine `dhcp.tp1.efrei`

- Commande utilisée : `sudo dnf install dhcp-server`

---

### 2. Installer et configurer un serveur DHCP

On met une ip statique: https://gitlab.com/it4lik/b2-network-virt/-/blob/main/memo/rocky_network.md

- Configuration utilisée :  
```
sudo dnf install -y dhcp-serveur
```
```
sudo nano /etc/dhcp/dhcpd.conf
```
```
authoritative;
subnet 10.1.1.0 netmask 255.255.255.0 {
    range 10.1.1.10 10.1.1.50;
    option broadcast-address 10.1.1.1;
    option routers 10.1.1.1;
}
```
```
sudo systemctl enabled dhcpd
```
```
sudo systemctl start dhcpd
```
```
sudo systemctl status dhcpd
```

### 3. Récupérer une IP automatiquement depuis les 3 nodes

#### Résultat :  
```
Node1> show ip
IP/MASK     : 10.1.1.10/24

Node2> show ip
IP/MASK     : 10.1.1.11/24

Node3> show ip
IP/MASK     : 10.1.1.12/24
```

### 4. Wireshark !

- Protocole DHCP capturé. Voir fichier joint : [wireshark_dora.pcapng](wireshark_dora.pcapng)

---

### 5. Configurer dnsmasq

- Configuration utilisée :
  
```
sudo dnf install dnsmasq -y
```
```
port=0 # pour désactiver DNS
dhcp-range=10.1.1.210,10.1.1.250,255.255.255.0,12h
dhcp-authoritative
interface=enp0s3
```

### 6. Test !
```
PC -> dhcp
DDORA IP 10.1.1.248
24 GW 10.1.1.50
```
```
PC -> show ip
```
NAME        : PC4[1]
IP/MASK     : 10.1.1.248/24

#### Résultat :  
```
IP attribuée par dnsmasq : 10.1.1.210
```

---

### 7. Now race !
```
machine 2 -> dhcp

DDORA IP 10.1.1.246/24 GW 10.1.1.50

Machine 3 -> dhcp

DDORA IP 10.1.1.247/24 GW 10.1.1.50

Machine 4 -> dhcp

DORA IP 10.1.1.21/24 GW 10.1.1.1
```



