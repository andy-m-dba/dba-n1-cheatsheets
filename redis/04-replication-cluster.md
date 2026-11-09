# REDIS-N1-04 — Réplication & cluster

**Quand ?** Replica déconnecté, failover, slots indisponibles.

### Dans redis-cli
```text
INFO replication
```

**Seulement en Redis Cluster** :
```text
CLUSTER INFO
```

### Lecture rapide
- `role` : `master` ou `slave` dans les champs Redis ; interpréter selon la topologie.
- `master_link_status:down` sur un réplica attendu : anomalie.
- `cluster_state:ok` : ce nœud voit un cluster utilisable ; ne garantit pas toute l'application.
- `cluster_state:fail`, `cluster_slots_fail > 0` : escalade immédiate.
- `CLUSTER INFO` est inapplicable en standalone et peut être bloqué par ACL.

**Escalade :** nœud, rôle, lien, slots, alerte et impact. Aucun `REPLICAOF`, `CLUSTER MEET` ou `FAILOVER` N1.

[Sources : INFO](https://redis.io/docs/latest/commands/info/) · [CLUSTER INFO](https://redis.io/docs/latest/commands/cluster-info/)
