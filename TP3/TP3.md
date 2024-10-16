### TP3 : 32°13'34"N 95°03'27"W

* I. ARP basics

☀️ Adresse MAC de ma carte WiFi : 

```
Carte réseau sans fil Wi-Fi :

   Adresse physique . . . . . . . . . . . : 2C-98-11-56-BF-F1
```
☀️ Affichez votre table ARP

```
PS C:\Windows\system32> arp -a

Interface : 10.33.78.249 --- 0x4
  Adresse Internet      Adresse physique      Type
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.76.78.75          01-00-5e-4c-4e-4b     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.56.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.76.78.75          01-00-5e-4c-4e-4b     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique

Interface : 192.168.131.1 --- 0x14
  Adresse Internet      Adresse physique      Type
  192.168.131.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.76.78.75          01-00-5e-4c-4e-4b     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.253       01-00-5e-7f-ff-fd     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école

```
10.33.79.254          7c-5a-1c-d3-d8-76     dynamique

```

☀️ Supprimez la ligne qui concerne la passerelle

Avant : 
```
PS C:\Windows\system32> arp -a

Interface : 10.33.78.249 --- 0x4
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
```

Après : 
```
PS C:\Windows\system32> arp -d 10.33.79.254
PS C:\Windows\system32> arp -a

Interface : 10.33.78.249 --- 0x4
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
```

☀️ Wireshark

[arp1](arp1.pcapng)

* II. ARP dans un réseau local

1. Basics

☀️ Déterminer

pour la carte réseau impliquée dans le partage de connexion (carte WiFi ?)

son adresse IP au sein du réseau local formé par le partage de co
```
Carte réseau sans fil Wi-Fi :
   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.7(préféré)
```

son adresse Mac
```
Carte réseau sans fil Wi-Fi :
   Adresse physique . . . . . . . . . . . : 2C-98-11-56-BF-F1
```

☀️ DIY

Avant :
```
PS C:\Windows\system32> ipconfig

Carte réseau sans fil Wi-Fi :

   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.7
```

Après :
```
PS C:\Windows\system32> ipconfig

Carte réseau sans fil Wi-Fi :

   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.9
```

☀️ Pingz !

Ping copain : 

```
PS C:\Windows\system32> ping 172.20.10.4

Envoi d’une requête 'Ping'  172.20.10.4 avec 32 octets de données :
Réponse de 172.20.10.4 : octets=32 temps=29 ms TTL=128
Réponse de 172.20.10.4 : octets=32 temps=39 ms TTL=128
Réponse de 172.20.10.4 : octets=32 temps=204 ms TTL=128
Réponse de 172.20.10.4 : octets=32 temps=58 ms TTL=128

Statistiques Ping pour 172.20.10.4:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 29ms, Maximum = 204ms, Moyenne = 82ms
```

Ping Google :

```
PS C:\Windows\system32> ping google.com

Envoi d’une requête 'ping' sur google.com [2a00:1450:4007:80c::200e] avec 32 octets de données :
Réponse de 2a00:1450:4007:80c::200e : temps=62 ms
Réponse de 2a00:1450:4007:80c::200e : temps=81 ms
Réponse de 2a00:1450:4007:80c::200e : temps=78 ms
Réponse de 2a00:1450:4007:80c::200e : temps=76 ms

Statistiques Ping pour 2a00:1450:4007:80c::200e:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 62ms, Maximum = 81ms, Moyenne = 74ms
```

2. ARP

☀️ Affichez votre table ARP !

```
PS C:\Windows\system32> arp -a

Interface : 172.20.10.9 --- 0x4
  Adresse Internet      Adresse physique      Type
  172.20.10.1           e6-b2-fb-e8-21-64     dynamique
  172.20.10.2           28-c5-d2-03-3c-2f     dynamique
  172.20.10.4           10-68-38-8e-2e-ef     dynamique
  172.20.10.15          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.77.77.77          01-00-5e-4d-4d-4d     statique
```

Après avoir supprimé :

```
PS C:\Windows\system32> arp -a

Interface : 172.20.10.9 --- 0x4
  Adresse Internet      Adresse physique      Type
  172.20.10.1           e6-b2-fb-e8-21-64     dynamique
  172.20.10.15          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.77.77.77          01-00-5e-4d-4d-4d     statique
```

☀️ Capture arp2.pcap

[arp2](arp2.pcapng)

3. Bonus : ARP poisoning


