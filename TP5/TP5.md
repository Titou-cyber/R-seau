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

* 1. Accès internet routeur

☀️ Déjà, prouvez que le routeur a un accès internet

```
[titou@routeur ~]$ ping www.ynov.com
PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=54 time=84.4 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=54 time=39.6 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=3 ttl=54 time=76.4 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=4 ttl=54 time=57.4 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=5 ttl=54 time=29.4 ms
^C
--- www.ynov.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4011ms
rtt min/avg/max/mdev = 29.402/57.442/84.375/20.918 ms
```

☀️ Activez le routage

```
[titou@routeur ~]$ cat /etc/resolv.conf
# Generated by NetworkManager
search home tp5.b1
nameserver 8.8.8.8
nameserver 1.1.1.1
```
```
[titou@routeur ~]$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=54 time=26.7 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=54 time=33.8 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=3 ttl=54 time=46.0 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=4 ttl=54 time=27.2 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3006ms
rtt min/avg/max/mdev = 26.740/33.430/46.009/7.775 ms
```

* 2. Accès internet clients

☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau

```
titou@client2:~$ cat /etc/netplan/01-network-manager-all.yaml
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp0s8:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        addresses: [1.1.1.1,1.0.0.1]
```

* III. Serveur SSH

☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH

```
[titou@routeur ~]$ sudo ss -lnpt | grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=1732,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=1732,fd=4))
```

☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert

```
[titou@routeur ~]$ sudo firewall-cmd --list-all | grep services
  services: cockpit dhcpv6-client ssh
```

* IV. Serveur DHCP

* A. Installation et configuration du serveur DHCP

☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1

installation du paquet qui contient le serveur DHCP

```
[titou@routeur ~]$ sudo dnf install dhcp-server -y
Last metadata expiration check: 5:46:53 ago on Mon 14 Oct 2024 10:33:51 AM CEST.
Dependencies resolved.
=========================================================================
 Package          Arch        Version                  Repository   Size
=========================================================================
Installing:
 dhcp-server      x86_64      12:4.4.2-19.b1.el9       baseos      1.2 M
Installing dependencies:
 dhcp-common      noarch      12:4.4.2-19.b1.el9       baseos      128 k

Transaction Summary
=========================================================================
Install  2 Packages

Total download size: 1.3 M
Installed size: 4.2 M
Downloading Packages:
(1/2): dhcp-common-4.4.2-19.b1.el9.noarc 589 kB/s | 128 kB     00:00
(2/2): dhcp-server-4.4.2-19.b1.el9.x86_6 2.9 MB/s | 1.2 MB     00:00
-------------------------------------------------------------------------
Total                                    2.0 MB/s | 1.3 MB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                 1/1
  Installing       : dhcp-common-12:4.4.2-19.b1.el9.noarch           1/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64           2/2
  Installing       : dhcp-server-12:4.4.2-19.b1.el9.x86_64           2/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64           2/2
  Verifying        : dhcp-server-12:4.4.2-19.b1.el9.x86_64           1/2
  Verifying        : dhcp-common-12:4.4.2-19.b1.el9.noarch           2/2

Installed:
  dhcp-common-12:4.4.2-19.b1.el9.noarch
  dhcp-server-12:4.4.2-19.b1.el9.x86_64

Complete!
```

modification de la configuration

```
  GNU nano 5.6.1             /etc/dhcp/dhcpd.conf                        #
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
#
# Option générale
option domain-name "tp5.b1";
option domain-name-servers 1.1.1.1;

# Paramètres du réseau
subnet 10.5.1.0 netmask 255.255.255.0 {
    range 10.5.1.137 10.5.1.237;
    option routers 10.5.1.254;
    option broadcast-address 10.5.1.255;
}
```

(re)démarrage du service DHCP 

```
[titou@routeur ~]$ sudo systemctl start dhcpd
```

* B. Test avec un nouveau client

☀️ Créez une nouvelle machine client client3.tp5.b1

Connections en SSH après avoir config ma VM client 3 

```
PS C:\Users\titou> ssh titou@10.5.1.137
titou@10.5.1.137's password:
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-45-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

31 updates can be applied immediately.
5 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Last login: Mon Oct 14 16:37:24 2024 from 10.5.1.1
```

Verif ip 

```
titou@client3:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e9:6a:da brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 41550sec preferred_lft 41550sec
    inet6 fe80::bc6:2ab5:9fb9:94c5/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

Connection internet instantanée

```
titou@client3:~$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=53 time=26.0 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=53 time=24.6 ms
64 bytes from 172.67.74.226: icmp_seq=3 ttl=53 time=26.2 ms
64 bytes from 172.67.74.226: icmp_seq=4 ttl=53 time=25.8 ms
^C
--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3022ms
rtt min/avg/max/mdev = 24.577/25.632/26.197/0.625 ms
```

* C. Consulter le bail DHCP

☀️ Consultez le bail DHCP qui a été créé pour notre client

```
[titou@routeur ~]$ sudo ls -l /var/lib/dhcpd/
[sudo] password for titou:
total 4
-rw-r--r--. 1 dhcpd dhcpd   0 Oct 26  2023 dhcpd6.leases
-rw-r--r--. 1 dhcpd dhcpd 581 Oct 14 16:28 dhcpd.leases
-rw-r--r--. 1 dhcpd dhcpd   0 Oct 26  2023 dhcpd.leases~
[titou@routeur ~]$ sudo cat /var/lib/dhcpd/dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

server-duid "\000\001\000\001.\237\345s\010\000't\020.";

lease 10.5.1.137 {
  starts 1 2024/10/14 14:28:12;
  ends 2 2024/10/15 02:28:12;
  cltt 1 2024/10/14 14:28:12;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:e9:6a:da;
  uid "\001\010\000'\351j\332";
  client-hostname "titou-VirtualBox";
}
```

☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e9:6a:da brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 40893sec preferred_lft 40893sec
    inet6 fe80::bc6:2ab5:9fb9:94c5/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

Les adresses mac sont identiques le serveur DHCP est maintenant fonctionel.