# DHCP
# 🌞 Prouver avec un VPCS

```
PC4> ip dhcp
DORA IP 10.3.2.10/24 GW 10.3.2.254

PC4> sh ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.10/24
GATEWAY     : 10.3.2.254
DNS         : 1.1.1.1
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 43184, 43200/21600/37800
MAC         : 00:50:79:66:68:03
LPORT       : 20029
RHOST:PORT  : 127.0.0.1:20030
MTU         : 1500

PC4> ping efrei.fr
efrei.fr resolved to 51.255.68.208

84 bytes from 51.255.68.208 icmp_seq=1 ttl=53 time=29.699 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=53 time=31.028 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=53 time=25.568 ms
84 bytes from 51.255.68.208 icmp_seq=4 ttl=53 time=28.295 ms
```
# DNS
### 🌞 Tests resolution DNS
```
PC4> dhcp
DORA IP 10.3.2.10/24 GW 10.3.2.254

PC4> sh ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.10/24
GATEWAY     : 10.3.2.254
DNS         : 10.3.3.1
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 41801, 42299/21149/37011
MAC         : 00:50:79:66:68:03
LPORT       : 20029
RHOST:PORT  : 127.0.0.1:20030
MTU         : 1500

PC4> ping efrei.fr
efrei.fr resolved to 51.255.68.208

84 bytes from 51.255.68.208 icmp_seq=1 ttl=53 time=29.676 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=53 time=24.036 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=53 time=28.247 ms
84 bytes from 51.255.68.208 icmp_seq=4 ttl=53 time=25.962 ms
84 bytes from 51.255.68.208 icmp_seq=5 ttl=53 time=32.531 ms

```