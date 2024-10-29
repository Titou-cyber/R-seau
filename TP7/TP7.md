### TP7 : On dit chiffrer pas crypter

* II. Serveur Web

🌞 Lister les ports en écoute sur la machine

```
[titou@web ~]$ sudo ss -lnpt | grep nginx
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=11222,fd=6),("nginx",pid=11221,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=11222,fd=7),("nginx",pid=11221,fd=7))
```

🌞 Ouvrir le port dans le firewall de la machine

```
[titou@web ~]$ sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --reload
success
success
```

C. Tests client

🌞 Vérifier que ça a pris effet

faites un ping vers sitedefou.tp7.b1

```
titou@client1:~$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=1.67 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=1.41 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=1.19 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=4 ttl=64 time=1.40 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 1.193/1.415/1.665/0.167 ms
```

visitez http://sitedefou.tp7.b1

```
titou@client1:~$ curl http://sitedefou.tp7.b1
meow !
```

🌞 Lister les ports en écoute sur la machine

```
[titou@web ~]$ sudo ss -lnpt | grep nginx
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1337,fd=6),("nginx",pid=1336,fd=6))
```

🌞 Gérer le firewall

```
[titou@web ~]$ sudo firewall-cmd --permanent --add-port=443/tcp
sudo firewall-cmd --reload
success
success
[titou@web ~]$ sudo firewall-cmd --permanent --remove-port=80/tcp        sudo firewall-cmd --reload
success
success
```

* III. Serveur VPN

🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0

```
[titou@vpn ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8a:66:09 brd ff:ff:ff:ff:ff:ff
    inet 10.7.1.111/24 brd 10.7.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe8a:6609/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s9: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ef:be:30 brd ff:ff:ff:ff:ff:ff
    inet 10.7.2.111/24 brd 10.7.2.255 scope global noprefixroute enp0s9
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feef:be30/64 scope link
       valid_lft forever preferred_lft forever
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

🌞 Déterminer sur quel port écoute Wireguard

```
[titou@vpn ~]$ sudo ss -lnpu | grep 51820
UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*
UNCONN 0      0               [::]:51820         [::]:*
```

🌞 Ouvrez ce port dans le firewall

```
[titou@vpn ~]$ sudo firewall-cmd --permanent --add-port=51820/tcp
sudo firewall-cmd --reload
success
success
```

* 3. Proofs

🌞 Ping ping ping !

depuis le client, faites un ping vers l'IP du serveur VPN au sein du réseau virtuel
donc ping 10.7.200.1

```
titou@client1:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
From 10.7.200.11 icmp_seq=1 Destination Host Unreachable
ping: sendmsg: Required key not available
From 10.7.200.11 icmp_seq=2 Destination Host Unreachable
ping: sendmsg: Required key not available
From 10.7.200.11 icmp_seq=3 Destination Host Unreachable
ping: sendmsg: Required key not available
From 10.7.200.11 icmp_seq=4 Destination Host Unreachable
ping: sendmsg: Required key not available

--- 10.7.200.1 ping statistics ---^C
4 packets transmitted, 0 received, +4 errors, 100% packet loss, time 3076ms
```

🌞 Capture ping1_vpn.pcap

capturez ces pings, en capturant sur l'interface host-ononly
ne vous attendez pas à vraiment voir directement des pings... vous regardez du trafic VPN

[Ping1](Ping1 tp7.pcap)

🌞 Capture ping2_vpn.pcap

capturez ces pings, en capturant sur l'interface wg0

vous allez voir vos vrais ping

[Ping2](ping2 tp7.pcap)

🌞 Prouvez que vous avez toujours un accès internet

```
titou@client1:~$ traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  _gateway (10.7.200.1)  4.009 ms  12.096 ms  12.083 ms
```

* 4. Private service

🌞 Visitez le service Web à travers le VPN

```
titou@client1:~$ curl -k https://sitedefou.tp7.b1
meow !
```