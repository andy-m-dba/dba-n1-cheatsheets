# REDIS-N1-03 — Clients & latence

**Quand ?** Connexions rejetées, lenteur, files d'attente.

### Dans redis-cli
```text
INFO clients
INFO stats
INFO commandstats
```

### Lecture rapide
- `connected_clients` / `maxclients` : comparer aux seuils locaux.
- `blocked_clients` : attente sur des commandes bloquantes ; peut être normal.
- `rejected_connections` : cumul depuis le démarrage/reset, comparer la tendance.
- `commandstats` : appels et temps passés par type de commande, pas latence réseau de bout en bout.
- Pour latence, consulter également la métrique applicative et la supervision.

**Escalade :** heure, nombre de clients, rejets, latence et impact. Ne pas lancer `CLIENT KILL`, `MONITOR` ou `SLOWLOG RESET` N1.

[Source : INFO](https://redis.io/docs/latest/commands/info/)
