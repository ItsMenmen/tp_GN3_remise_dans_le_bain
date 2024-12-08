
# Compte Rendu TP1 : Remise dans le bain

### 1. Déterminer l'adresse MAC de vos deux machines

- **pc1** : `00:50:79:66:68:00`
- **pc2** : `00:50:79:66:68:01`

---

### 2. Définir une IP statique sur les deux machines

- **pc1** : `10.1.1.1/24`  
- **pc2** : `10.1.1.2/24`  

---

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

- **pc1** : `00:50:79:66:68:00`
- **pc2** : `00:50:79:66:68:01`
- **pc3** : `00:50:79:66:68:02`

---

### 2. Définir une IP statique sur les trois machines

- **pc1** : `10.1.1.1/24`  
- **pc2** : `10.1.1.2/24`  
- **pc3** : `10.1.1.3/24`  

---

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

- Configuration utilisée :  
```
range 10.1.1.10 10.1.1.50;
option routers 10.1.1.254;
option subnet-mask 255.255.255.0;
```

---

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

---

### 4. Wireshark !

- Protocole DHCP capturé. Voir fichier joint : `wireshark_dora.pcapng`.

---

### 5. Configurer dnsmasq

- Configuration utilisée :  
```
dhcp-range=10.1.1.210,10.1.1.250,255.255.255.0,12h
```

---

### 6. Test !

#### Résultat :  
```
IP attribuée par dnsmasq : 10.1.1.210
```

---

### 7. Now race !

- Les deux serveurs DHCP répondent, mais dnsmasq attribue une IP dans certains cas.

---

### 8. Wireshark !

- Protocole capturé. Voir fichier joint : `dhcp_spoofing_race.pcapng`.

---

**Fin du compte rendu.**
