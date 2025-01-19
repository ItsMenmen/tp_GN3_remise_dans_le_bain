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

84 bytes from 51.255.68.208 icmp_seq=1 ttl=53 time=39.999 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=53 time=28.390 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=53 time=22.898 ms


PC4> ping dns.tp3.b2
dns.tp3.b2 resolved to 10.3.3.1

84 bytes from 10.3.3.1 icmp_seq=1 ttl=63 time=18.376 ms
84 bytes from 10.3.3.1 icmp_seq=2 ttl=63 time=20.828 ms
84 bytes from 10.3.3.1 icmp_seq=3 ttl=63 time=11.618 ms
84 bytes from 10.3.3.1 icmp_seq=4 ttl=63 time=15.048 ms
84 bytes from 10.3.3.1 icmp_seq=5 ttl=63 time=15.197 ms
```
# capture wireshark
[preuveDNS.pcapng](preuve_ping.pcapng)

# HTTP
### 🌞 Preuve avec un client

```
root@debian:/home/julien# curl web.tp3.b2 | head

 % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                Dload  Upload   Total   Spent    Left  Speed
  0    0       0       0         0      0        0  --:--:--  --:--:--  --:--:--   0
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
      html {
100  7620  100  7620     0      0   45863      0  --:--:--  --:--:--  --:--:-- 46181

```