# C8 – Documenter une infrastructure de production

## Schéma d'architecture globale

```
[Navigateur]
     |
     | http://localhost:8080 (PHP)
     | http://localhost:8081 (phpMyAdmin)
     |
[Docker Network : c7-infra-production_default]
     |
     +---> [web] php:8.2-apache (port 80 interne → 8080 externe)
     |          Volume : ./www → /var/www/html
     |
     +---> [phpmyadmin] phpmyadmin/phpmyadmin (port 80 interne → 8081 externe)
     |          Connecté à : db
     |
     +---> [db] mysql:8.0 (port 3306 interne)
                Volume persistant : db_data → /var/lib/mysql
```

---

## Plan d'adressage

| Service | Réseau Docker | Port externe | Port interne |
|---------|--------------|-------------|-------------|
| web (Apache/PHP) | c7-infra-production_default | 8080 | 80 |
| phpmyadmin | c7-infra-production_default | 8081 | 80 |
| db (MySQL) | c7-infra-production_default | — | 3306 |

---

## Plan de routage

Les containers communiquent entre eux via le réseau interne Docker `c7-infra-production_default`. Depuis l'extérieur, seuls les ports 8080 et 8081 sont exposés. MySQL n'est pas accessible directement depuis l'hôte.

| Source | Destination | Port | Autorisé |
|--------|------------|------|---------|
| Navigateur hôte | web | 8080 | ✅ |
| Navigateur hôte | phpmyadmin | 8081 | ✅ |
| Navigateur hôte | db | 3306 | ❌ (non exposé) |
| phpmyadmin | db | 3306 | ✅ (réseau interne) |
| web | db | 3306 | ✅ (réseau interne) |

---

## Credentials

| Service | Utilisateur | Mot de passe |
|---------|------------|-------------|
| MySQL root | root | root |
| MySQL app | user | password |
| Base de données | — | monsite |
