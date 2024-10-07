#TP1 : Les premiers pas de bébé B1

🌞 Adresses IP de ta machine

PS C:\Users\titou> ipconfig

Carte réseau sans fil Wi-Fi :

   Adresse IPv4. . . . . . . . . . . . . .: 10.33.78.249


PS C:\Users\titou> ipconfig

Carte Ethernet Ethernet 2 :

   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1

🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...

PS C:\Users\titou> ipconfig

Carte réseau sans fil Wi-Fi :

   Passerelle par défaut. . . . . . . . . : 10.33.79.254

PS C:\Users\titou> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
                                       PS C:\Users\titou> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
  
🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine

PS C:\Users\titou> Netsh advfirewall show allprofiles

Paramètres Profil de domaine :
----------------------------------------------------------------------
État                                  Actif
Stratégie de pare-feu                 BlockInbound,AllowOutbound
LocalFirewallRules                    N/A (magasin d'objets de stratégie de groupe uniquement)
LocalConSecRules                      N/A (magasin d'objets de stratégie de groupe uniquement)
InboundUserNotification               Activer
RemoteManagement                      Désactiver
UnicastResponseToMulticast            Activer

Journalisation :
LogAllowedConnections                 Désactiver
LogDroppedConnections                 Désactiver
FileName                              %systemroot%\system32\LogFiles\Firewall\pfirewall.log
MaxFileSize                           4096


Paramètres Profil privé :
----------------------------------------------------------------------
État                                  Actif
Stratégie de pare-feu                 BlockInbound,AllowOutbound
LocalFirewallRules                    N/A (magasin d'objets de stratégie de groupe uniquement)
LocalConSecRules                      N/A (magasin d'objets de stratégie de groupe uniquement)
InboundUserNotification               Activer
RemoteManagement                      Désactiver
UnicastResponseToMulticast            Activer

Journalisation :
LogAllowedConnections                 Désactiver
LogDroppedConnections                 Désactiver
FileName                              %systemroot%\system32\LogFiles\Firewall\pfirewall.log
MaxFileSize                           4096


Paramètres Profil public :
----------------------------------------------------------------------
État                                  Actif
Stratégie de pare-feu                 BlockInbound,AllowOutbound
LocalFirewallRules                    N/A (magasin d'objets de stratégie de groupe uniquement)
LocalConSecRules                      N/A (magasin d'objets de stratégie de groupe uniquement)
InboundUserNotification               Activer
RemoteManagement                      Désactiver
UnicastResponseToMulticast            Activer

Journalisation :
LogAllowedConnections                 Désactiver
LogDroppedConnections                 Désactiver
FileName                              %systemroot%\system32\LogFiles\Firewall\pfirewall.log
MaxFileSize                           4096

Ok.

II. Utiliser le réseau

🌞 Envoie un ping vers...

toi-même !

PS C:\Users\titou> ping 10.33.78.249

Envoi d’une requête 'Ping'  10.33.78.249 avec 32 octets de données :
Réponse de 10.33.78.249 : octets=32 temps<1ms TTL=128
Réponse de 10.33.78.249 : octets=32 temps<1ms TTL=128
Réponse de 10.33.78.249 : octets=32 temps<1ms TTL=128
Réponse de 10.33.78.249 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.78.249:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

🌞 Envoie un ping vers...

vers l'adresse IP 127.0.0.1

PS C:\Users\titou> ping 127.0.0.1

Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

🌞 On continue avec ping. Envoie un ping vers...

ta passerelle

PS C:\Users\titou> ping 10.33.79.254

Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
    Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),

un(e) pote sur le réseau

 ping 10.33.66.78

Envoi d’une requête 'Ping'  10.33.66.78 avec 32 octets de données :
Réponse de 10.33.66.78 : octets=32 temps=41 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=58 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=62 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=78 ms TTL=64

Statistiques Ping pour 10.33.66.78:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 41ms, Maximum = 78ms, Moyenne = 59ms

un site internet

PS C:\Users\titou> ping www.thinkerview.com

Envoi d’une requête 'ping' sur www.thinkerview.com [188.114.96.7] avec 32 octets de données :
Réponse de 188.114.96.7 : octets=32 temps=15 ms TTL=55
Réponse de 188.114.96.7 : octets=32 temps=16 ms TTL=55
Réponse de 188.114.96.7 : octets=32 temps=18 ms TTL=55
Réponse de 188.114.96.7 : octets=32 temps=19 ms TTL=55

Statistiques Ping pour 188.114.96.7:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 15ms, Maximum = 19ms, Moyenne = 17ms

🌞 Faire une requête DNS à la main

PS C:\Users\titou> nslookup
Serveur par dÚfaut :   dns.google
Address:  8.8.8.8

> www.thinkerview.com
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.thinkerview.com
Addresses:  2a06:98c1:3121::7
          2a06:98c1:3120::7
          188.114.97.7
          188.114.96.7

> www.wikileaks.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    wikileaks.org
Addresses:  80.81.248.21
          51.159.197.136
Aliases:  www.wikileaks.org

> www.torproject.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.torproject.org
Addresses:  2a01:4f9:c010:19eb::1
          2620:7:6002:0:466:39ff:fe7f:1826
          2620:7:6002:0:466:39ff:fe32:e3dd
          2a01:4f8:fff0:4f:266:37ff:feae:3bbc
          2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
          116.202.120.165
          204.8.99.144
          116.202.120.166
          204.8.99.146
          95.216.163.36

III. Sniffer le réseau

IV. Network scanning et adresses IP

🌞 Effectue un scan du réseau auquel tu es connecté

PS C:\Users\titou> nmap -sn -PR 10.33.64.0/20
Starting Nmap 7.95 ( https://nmap.org ) at 2024-09-27 11:54 Paris, Madrid (heure dÆÚtÚ)
Stats: 0:00:05 elapsed; 0 hosts completed (0 up), 4095 undergoing ARP Ping Scan
ARP Ping Scan Timing: About 4.22% done; ETC: 11:56 (0:01:53 remaining)
Stats: 0:01:22 elapsed; 0 hosts completed (0 up), 4095 undergoing ARP Ping Scan
ARP Ping Scan Timing: About 53.68% done; ETC: 11:56 (0:01:12 remaining)
Nmap scan report for 10.33.66.78
Host is up (0.065s latency).
MAC Address: E4:B3:18:48:36:68 (Intel Corporate)
Nmap scan report for 10.33.67.113
Host is up (0.20s latency).
MAC Address: D2:91:DE:DF:9A:6E (Unknown)
Nmap scan report for 10.33.69.68
Host is up (0.27s latency).
MAC Address: EE:E8:D9:89:3F:F1 (Unknown)
Nmap scan report for 10.33.69.89
Host is up (0.66s latency).
MAC Address: AC:C9:06:10:14:B6 (Apple)
Nmap scan report for 10.33.69.90
Host is up (0.018s latency).
MAC Address: 60:E9:AA:DD:EE:4D (Cloud Network Technology Singapore PTE.)
Nmap scan report for 10.33.69.92
Host is up (0.066s latency).
MAC Address: D2:8A:D4:B4:A0:6E (Unknown)
Nmap scan report for 10.33.69.96
Host is up (0.30s latency).
MAC Address: 3E:59:E5:D6:30:1F (Unknown)
Nmap scan report for 10.33.69.102
Host is up (1.2s latency).
MAC Address: F6:F2:C4:53:28:F5 (Unknown)
Nmap scan report for 10.33.69.124
Host is up (0.011s latency).
MAC Address: CC:08:FA:83:C8:7B (Apple)
Nmap scan report for 10.33.69.132
Host is up (0.12s latency).
MAC Address: 4C:44:5B:41:6B:B7 (Intel Corporate)

🌞 Changer d'adresse IP

PS C:\Users\titou> ipconfig

Carte réseau sans fil Wi-Fi :

  IPv4. . . . . . . . . . . . . .: 10.33.77.171
