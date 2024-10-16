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