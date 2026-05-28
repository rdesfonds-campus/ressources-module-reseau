# Commandes de base Linux — Réseau

> Toutes ces commandes s'exécutent dans un terminal Linux (Bash).

---

## Commandes de diagnostic réseau

### `ip a` (ou `ip addr`)
Affiche toutes les interfaces réseau et leurs configurations : adresse IP, masque, adresse MAC, état.

```bash
ip a                        # Liste toutes les interfaces
ip a show enp0s31f6         # Détail d'une interface spécifique
```

**Lire la sortie :**
- `state UP` → interface active
- `inet 192.168.1.10/24` → adresse IP et masque
- `link/ether 00:1a:2b:3c:4d:5e` → adresse MAC

---

### `ip route show`
Affiche la table de routage : passerelle par défaut et routes connues.

```bash
ip route show               # Affiche toutes les routes
```

**Lire la sortie :**
- `default via 192.168.1.254` → passerelle par défaut
- `dev enp0s31f6` → interface utilisée

---

### `ping`
Teste la connectivité entre deux machines via des paquets ICMP.

```bash
ping google.com             # Ping en continu (CTRL+C pour arrêter)
ping -c 4 google.com        # Envoie exactement 4 paquets
ping -c 4 8.8.8.8           # Teste Internet sans résolution DNS
ping -c 4 192.168.1.254     # Teste la passerelle locale
```

**Lire les statistiques :**
- `4 packets transmitted, 4 received, 0% packet loss` → connexion parfaite
- `packet loss > 0%` → instabilité réseau
- `Destination Host Unreachable` → machine injoignable

---

### `traceroute`
Affiche le chemin (liste des routeurs) emprunté pour atteindre une destination.

```bash
traceroute google.com           # Trace le chemin vers google.com
traceroute 8.8.8.8              # Trace le chemin vers l'IP 8.8.8.8
```

Si non installé :
```bash
sudo apt install traceroute -y
```

Chaque ligne = un saut (nœud réseau). `* * *` = routeur qui ne répond pas aux sondes.

---

### `nslookup`
Interroge le serveur DNS pour résoudre un nom de domaine en adresse IP.

```bash
nslookup google.com             # Résout google.com → adresse IP
nslookup 8.8.8.8                # Reverse DNS : IP → nom de domaine
```

---

### `dig`
Outil avancé de requête DNS, plus détaillé que nslookup.

```bash
dig google.com                  # Résolution DNS complète
dig google.com +short           # Juste l'adresse IP
```

---

### `netstat` / `ss`
Affiche les connexions réseau actives et les ports en écoute. `ss` est le remplaçant moderne de `netstat`.

```bash
ss -tuln                        # Ports TCP/UDP en écoute
ss -tan                         # Toutes les connexions TCP
netstat -tuln                   # Equivalent avec netstat (si installé)
```

---

### `curl`
Envoie une requête HTTP depuis le terminal. Utile pour tester qu'un serveur web répond.

```bash
curl https://google.com         # Récupère le contenu de la page
curl -I https://google.com      # Affiche uniquement les en-têtes HTTP
curl -v https://google.com      # Mode verbose, détail complet de la requête
```

---

## Commandes système utiles

### `cat`, `head`, `tail`
Lire des fichiers de logs ou de configuration réseau.

```bash
cat /etc/hosts                  # Fichier de résolution DNS locale
cat /etc/resolv.conf            # Serveurs DNS configurés sur la machine
head -n 20 /var/log/syslog      # 20 premières lignes du log système
tail -n 20 /var/log/syslog      # 20 dernières lignes (les plus récentes)
tail -f /var/log/syslog         # Suivi en temps réel du log
```

---

## Récapitulatif rapide

| Commande | Usage principal |
|----------|----------------|
| `ip a` | Voir l'IP, masque, MAC de toutes les interfaces |
| `ip route show` | Voir la passerelle par défaut |
| `ping -c 4 8.8.8.8` | Tester si Internet est accessible |
| `ping -c 4 192.168.x.x` | Tester si la passerelle locale répond |
| `traceroute 8.8.8.8` | Voir les routeurs traversés pour atteindre Internet |
| `nslookup google.com` | Vérifier que la résolution DNS fonctionne |
| `ss -tuln` | Voir les ports ouverts sur la machine |
| `curl -I https://google.com` | Tester qu'un serveur web répond |
| `cat /etc/resolv.conf` | Voir les serveurs DNS configurés |
