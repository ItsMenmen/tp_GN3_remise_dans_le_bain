# VLANS
# 🌞 Tests de ping

```
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.3.1.1/24
GATEWAY     : 10.3.1.254
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:20001
MTU         : 1500
```

```
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=0.731 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=0.978 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=0.895 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=0.929 ms
84 bytes from 10.3.1.2 icmp_seq=5 ttl=64 time=1.128 ms
```
# ➜ Configuration IP du routeur
### 🌞 Tests de ping
```
R1#ping 10.3.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/33/36 ms
```
```
R1#ping 10.3.2.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.2.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/32/36 ms
```

```
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.3.1.1/24
GATEWAY     : 10.3.1.254
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:20001
MTU         : 1500
```
```
PC1> ping 10.3.1.254

84 bytes from 10.3.1.254 icmp_seq=1 ttl=255 time=8.945 ms
84 bytes from 10.3.1.254 icmp_seq=2 ttl=255 time=4.211 ms
84 bytes from 10.3.1.254 icmp_seq=3 ttl=255 time=3.678 ms
84 bytes from 10.3.1.254 icmp_seq=4 ttl=255 time=2.049 ms
84 bytes from 10.3.1.254 icmp_seq=5 ttl=255 time=4.807 ms
```
```
PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.3.2.1/24
GATEWAY     : 255.255.255.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 20002
RHOST:PORT  : 127.0.0.1:20003
MTU         : 1500
```

```
PC2> ping 10.3.1.254

84 bytes from 10.3.1.254 icmp_seq=1 ttl=255 time=10.164 ms
84 bytes from 10.3.1.254 icmp_seq=2 ttl=255 time=0.928 ms
84 bytes from 10.3.1.254 icmp_seq=3 ttl=255 time=7.183 ms
84 bytes from 10.3.1.254 icmp_seq=4 ttl=255 time=5.015 ms
84 bytes from 10.3.1.254 icmp_seq=5 ttl=255 time=3.202 ms
```

# ➜ Configuration du NAT
### 🌞 Tests de ping
```
R1#ping 8.8.8.8

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 8.8.8.8, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 64/88/120 ms
```
```
PC1> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=114 time=33.582 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=114 time=26.412 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=114 time=29.865 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=114 time=39.409 ms
84 bytes from 8.8.8.8 icmp_seq=5 ttl=114 time=44.824 ms
```
```
PC2> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=114 time=24.660 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=114 time=41.296 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=114 time=35.231 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=114 time=22.814 ms
84 bytes from 8.8.8.8 icmp_seq=5 ttl=114 time=32.782 ms
```