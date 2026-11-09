# REDIS-N1-04 — Réplication & cluster

**Quand ?** Réplica déconnecté, bascule inattendue ou slots indisponibles.

### Dans redis-cli
```text
INFO replication
```

### Uniquement sur Redis Cluster
```text
CLUSTER INFO
```

### Lecture rapide
- `role` : `master` (primaire) ou `slave` (réplica) dans la sortie Redis.
- Sur un réplica, `master_link_status:down` est suspect si le lien doit être actif.
- En cluster, `cluster_slots_assigned` attendu : **16384** ; confronter à l'architecture.
- `cluster_state:fail` ou `cluster_slots_fail > 0` : escalader immédiatement.
- `cluster_state:ok` décrit la vue du nœud, sans garantir tout le parcours applicatif.
- `CLUSTER INFO` n'est pas applicable en standalone et peut être refusé par ACL.

**Escalade :** nœud, rôle, état du lien, slots, heure et impact. Aucun `REPLICAOF`, `CLUSTER MEET` ou `FAILOVER` N1.

[Sources : INFO](https://redis.io/docs/latest/commands/info/) · [CLUSTER INFO](https://redis.io/docs/latest/commands/cluster-info/)
