# PG-N1-04 — Réplication physique

**Quand ?** Standby absent, connexion de réplication perdue, alerte de retard.

### Rôle du nœud

```sql
SELECT pg_is_in_recovery() AS standby;
```

### Sur le primaire : émetteurs WAL connectés

```sql
SELECT application_name, state, sync_state,
       write_lag, flush_lag, replay_lag
FROM pg_stat_replication;
```

### Sur le standby : réception WAL

```sql
SELECT status, last_msg_receipt_time, latest_end_time
FROM pg_stat_wal_receiver;
```

### Lecture rapide

- `streaming` signifie connexion en flux, pas nécessairement réplica à jour.
- Aucune ligne n'est anormale **que si** un émetteur/récepteur est attendu.
- Les champs `*_lag` peuvent être `NULL` ; ils ne prédisent pas le rattrapage.
- Valider la topologie attendue avec l'inventaire et l'outil HA.

**Escalade :** nœud concerné, état attendu/observé, heure, supervision. **Jamais de promotion ou failover N1.**

[Référence : vues de réplication](https://www.postgresql.org/docs/current/monitoring-stats.html)
