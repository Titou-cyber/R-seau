### TP2 : Hey yo tell a neighbor tell a friend

1. Quelques pings

* PS C:\Windows\System32> Get-NetIPAddress -InterfaceAlias "Ethernet"

'''
 IPAddress         : fe80::f17:1113:dcc7:3e5c%11
 InterfaceIndex    : 11
 InterfaceAlias    : Ethernet
 AddressFamily     : IPv6
 Type              : Unicast
 PrefixLength      : 64
 PrefixOrigin      : WellKnown
 SuffixOrigin      : Link
 AddressState      : Preferred
 ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
 PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
 SkipAsSource      : False
 PolicyStore       : ActiveStore

 IPAddress         : 10.67.69.133
 InterfaceIndex    : 11
 InterfaceAlias    : Ethernet
 AddressFamily     : IPv4
 Type              : Unicast
 PrefixLength      : 24
 PrefixOrigin      : Manual
 SuffixOrigin      : Manual
 AddressState      : Preferred
 ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
 PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
 SkipAsSource      : False
 PolicyStore       : ActiveStore
'''

PS C:\Windows\System32> ping 10.67.69.132

Envoi d’une requête 'Ping'  10.67.69.132 avec 32 octets de données :
Réponse de 10.67.69.132 : octets=32 temps=3 ms TTL=128
Réponse de 10.67.69.132 : octets=32 temps=2 ms TTL=128
Réponse de 10.67.69.132 : octets=32 temps=3 ms TTL=128
Réponse de 10.67.69.132 : octets=32 temps=2 ms TTL=128

Statistiques Ping pour 10.67.69.132:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 2ms, Maximum = 3ms, Moyenne = 2ms

PS C:\Users\rapha\Downloads\netcat-1.11> .\nc.exe 10.67.69.232 9999
test
hello 
coucou


PS C:\Users\rapha\Downloads\netcat-1.11> netstat -a -n -b

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.33.70.238:9999      10.33.68.254:29873     ESTABLISHED

je deviens pc server :

PS C:\Users\rapha\Downloads\netcat-1.11> netstat -b -a

Connexions actives

  TCP    0.0.0.0:9999           LAPTOP-MMJBVRQM:0      LISTENING
 [nc64.exe]
PS C:\Users\rapha\Downloads\netcat-1.11> ./nc64.exe -l -p 9999
salut
coucou
PS C:\Users\rapha\Downloads\netcat-1.11> netstat -b -n

Connexions actives

  TCP    10.67.69.133:9999      10.67.69.132:27021     ESTABLISHED
 [nc64.exe]

### III. Analyse de vos applications usuelles

1. Serveur web

HTTP.pcapng a l'appui

2. Autres services

Youtube sur netstat :  
[msedge.exe]
UDP    0.0.0.0:51365          91.68.245.16:443

Steam sur nestat : 
[Among Us.exe]
TCP    192.168.1.50:14106     13.69.141.149:443      ESTABLISHED

Discord sur netstat :
[Discord.exe]
TCP    192.168.1.50:15260     162.159.135.232:443    ESTABLISHED

Outlook sur netstat : 

[olk.exe]
TCP    [2a01:cb19:a23:f00:5c0e:7b8:fb99:dc1]:18123  [2620:1ec:c11::239]:443  ESTABLISHED

LenovoVantage sur netstat : 

[LenovoVantageService.exe]
TCP    192.168.1.50:18252     2.22.57.22:443         ESTABLISHED

