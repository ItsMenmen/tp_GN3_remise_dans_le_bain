# 🌞 ping d'un client du LAN1 vers un client du LAN 2
  

```
PC2> ping 10.3.2.2

84 bytes from 10.3.2.2 icmp_seq=1 ttl=62 time=41.091 ms
84 bytes from 10.3.2.2 icmp_seq=2 ttl=62 time=21.023 ms
84 bytes from 10.3.2.2 icmp_seq=3 ttl=62 time=31.019 ms
84 bytes from 10.3.2.2 icmp_seq=4 ttl=62 time=38.920 ms
84 bytes from 10.3.2.2 icmp_seq=5 ttl=62 time=25.151 ms
```

🌞 Capture Wireshark 
[ping_partie1.pcapng](ping_partie1.pcapng)

# 🌞 Afficher les adresses MAC des routeurs
```
R1#show arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  10.3.12.1               -   c401.05b0.0000  ARPA   FastEthernet0/0
Internet  10.3.12.2              47   c402.05ad.0000  ARPA   FastEthernet0/0
Internet  10.3.1.1               18   0050.7966.6800  ARPA   FastEthernet0/1
Internet  10.3.1.2                9   0050.7966.6801  ARPA   FastEthernet0/1
Internet  10.3.1.3               14   0050.7966.6800  ARPA   FastEthernet0/1
Internet  192.168.122.1           5   5254.0024.5d50  ARPA   FastEthernet1/0
Internet  192.168.122.148         -   c401.05b0.0010  ARPA   FastEthernet1/0
Internet  10.3.1.254              -   c401.05b0.0001  ARPA   FastEthernet0/1
```
```
R2#show arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  10.3.12.1              48   c401.05b0.0000  ARPA   FastEthernet0/0
Internet  10.3.12.2               -   c402.05ad.0000  ARPA   FastEthernet0/0
Internet  10.3.2.2               10   0050.7966.6803  ARPA   FastEthernet1/0
Internet  10.3.2.1               16   0050.7966.6802  ARPA   FastEthernet1/0
Internet  10.3.2.254              -   c402.05ad.0010  ARPA   FastEthernet1/0
```

# 🌞 Prouvez que vous avez déjà un accès internet sur r1
```
R1#ping 8.8.8.8

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 8.8.8.8, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 60/64/68 ms
```