# C6 – Connaître les outils de test et de diagnostic des réseaux IP

## Objectif
Valider que Google.com / 8.8.8.8 est joignable et lister les routeurs traversés pour y arriver.

---

## 1. Test de connectivité Internet — `ping`

```powershell
ping -n 4 8.8.8.8
```

- 4 paquets envoyés, 4 reçus, 0% de perte
- Latence moyenne : 10ms
- **Conclusion : Internet accessible**

```powershell
ping google.com
```

- Résolution DNS fonctionnelle → google.com résolu en `2a00:1450:4007:805::200e`
- 4 paquets envoyés, 4 reçus, 0% de perte
- Latence moyenne : 10ms

![ping google.com et 8.8.8.8](6.1-ping-google.png)

---

## 2. Tracé de route vers Google — `tracert`

```powershell
tracert 8.8.8.8
```

Liste les routeurs successifs traversés pour atteindre le serveur DNS de Google.

![tracert 8.8.8.8](6.2-tracert-google.png)
