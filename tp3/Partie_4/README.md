## 1. DNS
# 🌞 **Requêter l'enregistrement AXFR**
```
root@debian:/home/julien# dig axfr @dns.tp3.b2 tp3.b2

; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> axfr @dns.tp3.b2 tp3.b2
; (1 server found)
;; global options: +cmd
tp3.b2.           86400   IN  SOA    dns.tp3.b2. admin.tp3.b2. 2024011902
tp3.b2.           86400   IN  NS     dns.tp3.b2.
dns.tp3.b2.       86400   IN  A      10.3.3.1
supersite.tp3.b2. 86400   IN  A      10.3.3.3
web.tp3.b2.       86400   IN  A      10.3.3.2
tp3.b2.           86400   IN  SOA    dns.tp3.b2. admin.tp3.b2. 2024011902

;; Query time: 44 msec
;; SERVER: 10.3.3.1#53(dns.tp3.b2) (TCP)
;; WHEN: Sun Jan 19 15:39:50 CST 2025
;; XFR size: 6 records (messages 1, bytes 221)
```
 
🌞 **Spoof DNS query**

🌞 **Mettre en place une attaque TCP RST**
