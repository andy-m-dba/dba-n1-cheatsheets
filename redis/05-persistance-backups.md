# REDIS-N1-05 — Persistance & sauvegardes

**Quand ?** Alerte RDB/AOF, snapshot absent ou risque de perte de données.

### Dans redis-cli
```text
INFO persistence
```

### Lecture rapide
- `rdb_last_bgsave_status:err` : dernier snapshot RDB en échec.
- `rdb_last_save_time` : heure Unix du dernier snapshot réussi ; comparer à la politique attendue.
- `aof_enabled:1` : AOF activé ; `aof_last_write_status:err` : dernière écriture AOF en échec.
- RDB/AOF désactivés peuvent être normaux pour un cache : vérifier l'usage réel.
- Ces indicateurs ne garantissent **ni backup externe ni restauration réussie** ; vérifier l'outil officiel.

**Escalade :** politique attendue, état RDB/AOF, dernière réussite, RPO et impact. Aucun `BGSAVE`, `BGREWRITEAOF` ou restauration N1.

[Source : INFO persistence](https://redis.io/docs/latest/commands/info/)
