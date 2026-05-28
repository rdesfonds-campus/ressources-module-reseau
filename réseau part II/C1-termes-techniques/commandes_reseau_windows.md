# Commandes de base Windows — Réseau

> Toutes ces commandes s'exécutent dans PowerShell ou l'Invite de commandes (cmd).

---

## Commandes de diagnostic réseau

### `ipconfig`
Affiche la configuration réseau de la machine : adresse IP, masque, passerelle.

```powershell
ipconfig              # Résumé de toutes les interfaces
ipconfig /all         # Détail complet (adresse MAC, DHCP, DNS, etc.)
ipconfig /release     # Libère l'adresse IP obtenue par DHCP
ipconfig /renew       # Demande une nouvelle adresse IP au serveur DHCP
ipconfig /flushdns    # Vide le cache DNS local
```

---

### `ping`
Teste la connectivité entre deux machines. Envoie des paquets ICMP et mesure le temps de réponse.

```powershell
ping google.com          # Teste la connectivité Internet (résolution DNS + réponse)
ping 8.8.8.8             # Teste la connectivité Internet (IP directe, sans DNS)
ping 192.168.1.1         # Teste la connectivité avec la passerelle locale
ping -n 10 google.com    # Envoie 10 paquets au lieu de 4 par défaut
ping -t google.com       # Ping en continu (CTRL+C pour arrêter)
```

**Lire les statistiques :**
- `Envoyés = 4, Reçus = 4, Perdus = 0` → connexion parfaite
- `Perdus > 0` → instabilité réseau
- `Délai d'expiration` → machine injoignable ou filtrée

---

### `tracert`
Affiche le chemin (liste des routeurs) emprunté par les paquets pour atteindre une destination.

```powershell
tracert google.com       # Trace le chemin vers google.com
tracert 8.8.8.8          # Trace le chemin vers l'IP 8.8.8.8
```

Chaque ligne correspond à un saut (nœud réseau). Le temps affiché est le délai vers ce nœud.

---

### `nslookup`
Interroge le serveur DNS pour résoudre un nom de domaine en adresse IP, ou l'inverse.

```powershell
nslookup google.com           # Résout google.com → adresse IP
nslookup 8.8.8.8              # Résout une IP → nom de domaine (reverse DNS)
nslookup google.com 1.1.1.1   # Interroge le serveur DNS 1.1.1.1 spécifiquement
```

---

### `netstat`
Affiche les connexions réseau actives et les ports en écoute.

```powershell
netstat -an          # Toutes les connexions et ports (numérique)
netstat -b           # Affiche le programme associé à chaque connexion
netstat -r           # Affiche la table de routage
```

---

### `arp`
Affiche ou modifie la table ARP (correspondances IP ↔ MAC connues de la machine).

```powershell
arp -a               # Affiche toutes les entrées ARP connues
```

---

## Récapitulatif rapide

| Commande | Usage principal |
|----------|----------------|
| `ipconfig /all` | Voir l'IP, masque, passerelle, DNS, MAC de la machine |
| `ping 8.8.8.8` | Tester si Internet est accessible |
| `ping 192.168.1.1` | Tester si la passerelle locale répond |
| `tracert 8.8.8.8` | Voir les routeurs traversés pour atteindre Internet |
| `nslookup google.com` | Vérifier que la résolution DNS fonctionne |
| `netstat -an` | Voir les connexions actives et ports ouverts |
| `arp -a` | Voir les machines connues sur le réseau local |
