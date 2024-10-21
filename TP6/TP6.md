### TP6 : Des bo services dans des bo LANs 

* I. Le setup

☀️ Prouvez que...

une machine du LAN1 peut joindre internet (ping un nom de domaine)

```
[titou@dhcp ~]$ ping google.com
PING google.com (142.251.37.174) 56(84) bytes of data.
64 bytes from mrs09s14-in-f14.1e100.net (142.251.37.174): icmp_seq=1 ttl=111 time=17.7 ms
64 bytes from mrs09s14-in-f14.1e100.net (142.251.37.174): icmp_seq=2 ttl=111 time=21.1 ms
64 bytes from mrs09s14-in-f14.1e100.net (142.251.37.174): icmp_seq=3 ttl=111 time=19.8 ms
64 bytes from mrs09s14-in-f14.1e100.net (142.251.37.174): icmp_seq=4 ttl=111 time=20.5 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 17.677/19.755/21.082/1.288 ms
```

une machine du LAN2 peut joindre internet (ping nom de domaine)

```
[titou@web ~]$ ping google.com
PING google.com (142.250.200.238) 56(84) bytes of data.
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=1 ttl=111 time=18.8 ms
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=2 ttl=111 time=19.2 ms
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=3 ttl=111 time=19.1 ms
64 bytes from mrs08s18-in-f14.1e100.net (142.250.200.238): icmp_seq=4 ttl=111 time=20.5 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 18.800/19.392/20.547/0.679 ms
```

une machine du LAN1 peut joindre une machine du LAN2 (ping une adresse IP)

```
[titou@dhcp ~]$ ping 10.6.2.11
PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=1 ttl=63 time=1.64 ms
64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=1.38 ms
64 bytes from 10.6.2.11: icmp_seq=3 ttl=63 time=1.88 ms
64 bytes from 10.6.2.11: icmp_seq=4 ttl=63 time=1.58 ms
^C
--- 10.6.2.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 1.384/1.620/1.881/0.177 ms
```

* II. LAN clients

☀️ Prouvez que...

le client a bien récupéré une adresse IP en DHCP

avec un ip a le mot-clé dynamic doit être écrit sur la ligne qui contient l'adresse IP
(y'a pas ce mot-clé quand tu définis une IP statique)

```
titou@client1:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:35:6c:d8 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 409sec preferred_lft 409sec
    inet6 fe80::1ae9:977f:992e:6549/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

vous avez bien 1.1.1.1 en DNS

commande dans le mémo pour consulter l'adresse IP du serveur DNS connu

```
titou@client1:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
        DNS Domain: tp6.b1
```

vous avez bien la bonne passerelle indiquée

idem, dans le mémo, pour afficher l'adresse de la passerelle actuellement configurée :


```
titou@client1:~$ ip route show
default via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100
10.6.1.0/24 dev enp0s8 proto kernel scope link src 10.6.1.37 metric 100
```

que ça ping un nom de domaine public sans problème magueule

```
titou@client1:~$ ping google.com
PING google.com (142.251.37.46) 56(84) bytes of data.
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=1 ttl=112 time=18.8 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=2 ttl=112 time=18.4 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=3 ttl=112 time=19.9 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=4 ttl=112 time=18.9 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3652ms
rtt min/avg/max/mdev = 18.419/18.986/19.853/0.529 ms
```

* III. LAN serveurzzzz

* III. 1. Serveur Web

3. Analyse et test

☀️ Déterminer sur quel port écoute le serveur NGINX

```
[titou@web ~]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1456,fd=6),("nginx",pid=1455,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1456,fd=7),("nginx",pid=1455,fd=7))
```

☀️ Ouvrir ce port dans le firewall

```
titou@client1:~$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/

      html {
        height: 100%;
        width: 100%;
      }
        body {
  background: rgb(20,72,50);
  background: -moz-linear-gradient(180deg, rgba(23,43,70,1) 30%, rgba(0,0,0,1) 90%)  ;
  background: -webkit-linear-gradient(180deg, rgba(23,43,70,1) 30%, rgba(0,0,0,1) 90%) ;
  background: linear-gradient(180deg, rgba(23,43,70,1) 30%, rgba(0,0,0,1) 90%);
  background-repeat: no-repeat;
  background-attachment: fixed;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#3c6eb4",endColorstr="#3c95b4",GradientType=1);
        color: white;
        font-size: 0.9em;
        font-weight: 400;
        font-family: 'Montserrat', sans-serif;
        margin: 0;
        padding: 10em 6em 10em 6em;
        box-sizing: border-box;

      }
```

* III. 2. Serveur DNS

4. Analyse du service

☀️ Déterminer sur quel(s) port(s) écoute le service BIND9

```
[titou@dns ~]$ sudo ss -lnpt | grep named
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1811,fd=22))
LISTEN 0      4096       127.0.0.1:953       0.0.0.0:*    users:(("named",pid=1811,fd=26))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=1811,fd=25))
LISTEN 0      4096           [::1]:953          [::]:*    users:(("named",pid=1811,fd=27))
```

☀️ Ouvrir ce(s) port(s) dans le firewall

```
[titou@dns ~]$ sudo firewall-cmd --permanent --add-port=53/tcp
sudo firewall-cmd --reload
success
success
[titou@dns ~]$ sudo firewall-cmd --permanent --add-port=953/tcp
success
[titou@dns ~]$ sudo firewall-cmd --reload
success
````

5. Tests manuels

☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps

```
[titou@dns ~]$ dig web.tp6.b1@10.6.2.12

; <<>> DiG 9.16.23-RH <<>> web.tp6.b1@10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 6699
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;web.tp6.b1\@10.6.2.12.         IN      A

;; AUTHORITY SECTION:
.                       86400   IN      SOA     a.root-servers.net. nstld.verisign-grs.com. 2024102100 1800 900 604800 86400

;; Query time: 50 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Oct 21 10:08:50 CEST 2024
;; MSG SIZE  rcvd: 124
```

```
[titou@dns ~]$ dig dns.tp6.b1@10.6.2.12

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1@10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 3255
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;dns.tp6.b1\@10.6.2.12.         IN      A

;; AUTHORITY SECTION:
.                       86400   IN      SOA     a.root-servers.net. nstld.verisign-grs.com. 2024102100 1800 900 604800 86400

;; Query time: 36 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Oct 21 10:14:15 CEST 2024
;; MSG SIZE  rcvd: 124
```

```
[titou@dns ~]$ dig ynov.com@10.6.2.12

; <<>> DiG 9.16.23-RH <<>> ynov.com@10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 33372
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;ynov.com\@10.6.2.12.           IN      A

;; AUTHORITY SECTION:
.                       86400   IN      SOA     a.root-servers.net. nstld.verisign-grs.com. 2024102100 1800 900 604800 86400

;; Query time: 38 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Oct 21 10:14:57 CEST 2024
;; MSG SIZE  rcvd: 122
```

```
[titou@dns ~]$ dig -x 10.6.2.11@10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11@10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 18231
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;12.2.6.11\@10.2.6.10.in-addr.arpa. IN  PTR

;; Query time: 21 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Oct 21 10:16:05 CEST 2024
;; MSG SIZE  rcvd: 61
```

```
[titou@dns ~]$ dig -x 10.6.2.12@10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12@10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 35453
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;12.2.6.12\@10.2.6.10.in-addr.arpa. IN  PTR

;; Query time: 23 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Oct 21 10:16:49 CEST 2024
;; MSG SIZE  rcvd: 61
```

☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1

```
titou@client1:~$ dig web.tp6.b1@10.6.2.12

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web.tp6.b1@10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 30685
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;web.tp6.b1\@10.6.2.12.         IN      A

;; AUTHORITY SECTION:
.                       86400   IN      SOA     a.root-servers.net. nstld.verisign-grs.com. 2024102100 1800 900 604800 86400

;; Query time: 46 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Oct 21 10:20:55 CEST 2024
;; MSG SIZE  rcvd: 124
```

☀️ Créez un nouveau client client2.tp6.b1 vitefé
récupérez une IP en DHCP sur ce nouveau client2.tp6.b1

```
titou@client2:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:69:cb:de brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.39/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 530sec preferred_lft 530sec
    inet6 fe80::82c4:5845:c11e:52c0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

vérifiez que vous avez bien 10.6.2.12 comme serveur DNS à contacter

```
titou@client2:~$ cat /etc/resolv.conf
# This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
# Do not edit.
#
# This file might be symlinked as /etc/resolv.conf. If you're looking at
# /etc/resolv.conf and seeing this text, you have followed the symlink.
#
# This is a dynamic resolv.conf file for connecting local clients to the
# internal DNS stub resolver of systemd-resolved. This file lists all
# configured search domains.
#
# Run "resolvectl status" to see details about the uplink DNS servers
# currently in use.
#
# Third party programs should typically not access this file directly, but only
# through the symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a
# different way, replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 10.6.2.12
options edns0 trust-ad
search tp6.b1
```
