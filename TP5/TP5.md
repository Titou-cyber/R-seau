### TP5 : Un ptit LAN à nous

* I. Setup

☀️ Uniquement avec des commandes, prouvez-que :

```
titou@client1:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bb:43:2e brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:febb:432e/64 scope link
       valid_lft forever preferred_lft forever
```

```
titou@client2:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:10:8d:1d brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe10:8d1d/64 scope link
       valid_lft forever preferred_lft forever
```

```
[titou@routeur ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8c:e5:c6 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 85396sec preferred_lft 85396sec
    inet6 fe80::a00:27ff:fe8c:e5c6/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:74:10:2e brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe74:102e/64 scope link
       valid_lft forever preferred_lft forever
```

* Ping routeur vers client : 

```
[titou@routeur ~]$ ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.736 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=1.30 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=2.17 ms
64 bytes from 10.5.1.11: icmp_seq=4 ttl=64 time=1.21 ms
^C
--- 10.5.1.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3008ms
rtt min/avg/max/mdev = 0.736/1.356/2.174/0.518 ms
[titou@routeur ~]$ ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=1.53 ms
64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=1.17 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=1.01 ms
64 bytes from 10.5.1.12: icmp_seq=4 ttl=64 time=1.14 ms
^C
--- 10.5.1.12 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3008ms
rtt min/avg/max/mdev = 1.013/1.214/1.531/0.192 ms
```

* Ping client1 vers client2 et routeur 

```
titou@client1:~$ ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=2.23 ms
64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=1.10 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=0.900 ms
64 bytes from 10.5.1.12: icmp_seq=4 ttl=64 time=1.06 ms
^C
--- 10.5.1.12 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3341ms
rtt min/avg/max/mdev = 0.900/1.322/2.233/0.531 ms
titou@client1:~$ ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.819 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=1.40 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.657 ms
64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=1.02 ms
^C
--- 10.5.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3015ms
rtt min/avg/max/mdev = 0.657/0.974/1.402/0.278 ms
```

* Ping client2 vers Client1 et routeur 

```
titou@client2:~$ ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.624 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.719 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.744 ms
64 bytes from 10.5.1.11: icmp_seq=4 ttl=64 time=0.915 ms
^C
--- 10.5.1.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3617ms
rtt min/avg/max/mdev = 0.624/0.750/0.915/0.105 ms
titou@client2:~$ ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.536 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=1.90 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.868 ms
64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=1.29 ms
^C
--- 10.5.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3033ms
rtt min/avg/max/mdev = 0.536/1.148/1.902/0.510 ms
```