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