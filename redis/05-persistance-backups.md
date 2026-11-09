# REDIS-N1-05 — Persistance & sauvegardes

**Quand ?** Alerte RDB, AOF, snapshot absent, risque de perte de données.

### Dans redis-cli
```text
INFO persistence
```

### Lecture rapide
- `rdb_last_bgsave_status` : statut du dernier snapshot RDB, **pas** une preuve de restaurabilité.
- `aof_last_write_status` : dernier état d'écriture AOF (si AOF actif).
- `rdb_last_save_time` / `rdb_last_bgsave_time_sec` : contextualiser avec la politique RDB.
- Persistance désactivée peut être **normale** pour un cache ; comparer à l'architecture.
- En service managé, vérifier aussi les backups dans la console autorisée.

**Escalade :** politique attendue, dernier résultat, RPO, alerte et impact. Aucun `BGSAVE`, `BGREWRITEAOF` ou restauration N1.

[Source : INFO persistence](https://redis.io/docs/latest/commands/info/)
