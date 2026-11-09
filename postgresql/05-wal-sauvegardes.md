# PG-N1-05 — WAL & sauvegardes

**Quand ?** Alerte archivage, job de sauvegarde échoué, risque d'accumulation WAL.

### Archivage natif PostgreSQL

```sql
SHOW archive_mode;

SELECT archived_count, failed_count,
       last_archived_time, last_failed_time, stats_reset
FROM pg_stat_archiver;
```

### Sauvegardes externes

Consulter **l'outil réellement utilisé** (pgBackRest, Barman, ordonnanceur, service managé) : dernier job, statut, heure et durée. Aucun `SELECT` PostgreSQL universel ne prouve la réussite de ces sauvegardes.

### Lecture rapide

- `archive_mode = off` peut être normal selon l'architecture.
- `failed_count` est cumulatif ; comparer deux points horodatés. Certains échecs ne sont pas comptés.
- Dernier WAL archivé ≠ sauvegarde restaurable. La restauration se vérifie par un test dédié.
- Comparer les alertes aux objectifs de sauvegarde définis localement.

**Escalade :** échec répété, retard de backup, espace WAL menacé. **Jamais de purge WAL, restauration ou modification d'archivage par N1.**

[Références : archivage](https://www.postgresql.org/docs/current/monitoring-stats.html) · [sauvegarde et PITR](https://www.postgresql.org/docs/current/continuous-archiving.html)
