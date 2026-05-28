# Glossaire Réseau

## Les types de réseaux

| Sigle | Nom | Description | Exemple concret |
|-------|-----|-------------|-----------------|
| PAN | Personal Area Network | Réseau personnel, très courte portée | Connexion Bluetooth entre un téléphone et une oreillette |
| LAN | Local Area Network | Réseau local, limité à un bâtiment | Réseau d'une maison ou d'une entreprise |
| MAN | Metropolitan Area Network | Réseau métropolitain, couvre une ville | Réseau d'un campus ou d'une ville |
| WAN | Wide Area Network | Réseau étendu, couvre de grandes distances | Internet (le plus grand WAN existant) |

---

## Les équipements réseau

| Équipement | Rôle | Couche OSI |
|------------|------|------------|
| **Câble Ethernet** | Support physique de transmission des données | Couche 1 – Physique |
| **Carte réseau (NIC)** | Interface entre la machine et le réseau, possède une adresse MAC | Couche 1/2 |
| **Switch** | Connecte plusieurs machines sur un même réseau local, transmet les trames selon les adresses MAC | Couche 2 – Liaison |
| **Routeur** | Relie des réseaux différents entre eux, achemine les paquets selon les adresses IP | Couche 3 – Réseau |
| **Point d'accès Wi-Fi** | Permet la connexion sans fil au réseau local | Couche 1/2 |

---

## Les adresses réseau

### Adresse MAC
Adresse physique unique gravée dans la carte réseau par le constructeur. Format : 6 octets en hexadécimal (ex : `00:1A:2B:3C:4D:5E`). Elle sert à identifier une machine dans un réseau local. Elle ne change pas et n'est pas routable entre réseaux.

### Adresse IP
Adresse logique qui identifie une machine sur un réseau. Elle peut être configurée manuellement (IP statique) ou attribuée automatiquement par un serveur DHCP. Elle est composée de 4 octets (IPv4), ex : `192.168.1.10`.

### Masque de sous-réseau
Définit quelle partie de l'adresse IP correspond au réseau et quelle partie correspond à la machine. Exemple : `255.255.255.0` (ou `/24`) signifie que les 3 premiers octets identifient le réseau, le dernier identifie la machine. Deux machines avec le même réseau peuvent communiquer directement ; sinon elles passent par un routeur.

### Passerelle par défaut (Gateway)
Adresse IP du routeur par lequel une machine envoie ses paquets quand la destination est hors de son réseau local.

### Adresse réseau
Première adresse d'une plage IP, réservée pour identifier le réseau lui-même. Ex : `192.168.1.0/24` → adresse réseau = `192.168.1.0`.

### Adresse de broadcast
Dernière adresse d'une plage IP, utilisée pour envoyer un message à toutes les machines du réseau. Ex : `192.168.1.0/24` → broadcast = `192.168.1.255`.

### DHCP (Dynamic Host Configuration Protocol)
Service qui attribue automatiquement une adresse IP, un masque, une passerelle et un serveur DNS aux machines qui se connectent au réseau.

---

## Les protocoles

### IP (Internet Protocol)
Protocole de la couche réseau. Gère l'adressage et le routage des paquets d'un réseau à un autre. Ne garantit pas la livraison.

### TCP (Transmission Control Protocol)
Protocole de transport fiable. Garantit que les données arrivent complètes et dans le bon ordre grâce à un système d'accusés de réception. Utilisé pour HTTP, SSH, FTP...

### UDP (User Datagram Protocol)
Protocole de transport rapide mais sans garantie de livraison. Utilisé quand la vitesse prime sur la fiabilité (streaming, jeux en ligne, DNS).

### ICMP (Internet Control Message Protocol)
Protocole utilisé pour envoyer des messages de contrôle réseau. C'est le protocole utilisé par la commande `ping`.

### DNS (Domain Name System)
Service qui fait la correspondance entre un nom de domaine lisible (ex : `google.com`) et une adresse IP. Sans DNS, il faudrait retenir les adresses IP de chaque site.

### HTTP / HTTPS
Protocole de communication du web. HTTP est non chiffré. HTTPS ajoute une couche de chiffrement TLS pour sécuriser les échanges.

---

## Le modèle OSI (7 couches)

| N° | Couche | Rôle | Équipements / Protocoles |
|----|--------|------|--------------------------|
| 7 | Application | Interface avec l'utilisateur | HTTP, DNS, FTP, SSH |
| 6 | Présentation | Encodage, chiffrement des données | TLS/SSL |
| 5 | Session | Gestion des sessions de communication | — |
| 4 | Transport | Découpage en segments, fiabilité | TCP, UDP |
| 3 | Réseau | Adressage et routage des paquets | IP, routeur |
| 2 | Liaison | Transmission dans le réseau local, adresses MAC | Switch, Ethernet |
| 1 | Physique | Transmission des bits sur le support physique | Câbles, Wi-Fi, NIC |

---

## Le modèle TCP/IP (4 couches)

| Couche TCP/IP | Correspond à (OSI) | Protocoles |
|---------------|-------------------|------------|
| Application | 5 + 6 + 7 | HTTP, DNS, SSH, FTP |
| Transport | 4 | TCP, UDP |
| Internet | 3 | IP, ICMP |
| Accès réseau | 1 + 2 | Ethernet, Wi-Fi |

---

## Autres termes clés

**Réseau** : Ensemble de machines reliées pour échanger des données ou partager des ressources.

**Internet** : Réseau mondial de réseaux, interconnectés via des routeurs et le protocole IP.

**Web** : Service qui fonctionne sur Internet, basé sur le protocole HTTP et accessible via un navigateur. Inventé au CERN par Tim Berners-Lee.

**Paquet** : Unité de données transmise sur un réseau IP. Chaque paquet contient l'adresse source, l'adresse destination et une portion des données.

**Port** : Numéro logique qui identifie un service sur une machine. Ex : port 80 = HTTP, port 443 = HTTPS, port 22 = SSH.

**Firewall (pare-feu)** : Système qui filtre le trafic réseau selon des règles pour protéger un réseau ou une machine.
