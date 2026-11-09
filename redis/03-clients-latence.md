# REDIS-N1-03 — Clients & latence

**Quand ?** Connexions rejetées, ralentissement ou temps de réponse élevé.

### Dans redis-cli
```text
INFO clients
INFO stats
INFO latencystats
```

### Lecture rapide
- `connected_clients` / `maxclients` : connexions actuelles et limite déclarée.
- `blocked_clients` : clients en attente d'une commande bloquante ; peut être normal.
- `rejected_connections` : connexions refusées **à cause de maxclients**, pas erreurs d'authentification ; comparer deux relevés.
- `latencystats` : percentiles de **latence des commandes Redis**, si suivi activé et métrique disponible ; pas le temps réseau ni applicatif.
- Vérifier les métriques de supervision pour connaître la latence de bout en bout.

**Escalade :** heure, nombre de clients, progression des rejets, percentiles et impact. Aucun `CLIENT KILL`, `MONITOR` ou changement de paramètres N1.

[Sources : INFO](https://redis.io/docs/latest/commands/info/) · [Limite des clients](https://redis.io/docs/latest/develop/reference/clients/)
