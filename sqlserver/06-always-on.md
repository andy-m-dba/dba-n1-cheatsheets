# MSSQL-N1-06 — Always On : état des réplicas

**Quand ?** Alerte Availability Group (AG), secondaire déconnecté ou désynchronisé.

### Réplicas de disponibilité
```sql
SELECT is_local, role_desc, connected_state_desc,
       synchronization_health_desc
FROM sys.dm_hadr_availability_replica_states;
```

### Bases de l'AG (sur le réplica local)
```sql
SELECT DB_NAME(database_id) AS base, is_primary_replica,
       synchronization_state_desc,
       synchronization_health_desc, is_suspended
FROM sys.dm_hadr_database_replica_states
WHERE is_local = 1;
```

### Lecture rapide
- `CONNECTED` ne signifie pas forcément `SYNCHRONIZED`.
- `SYNCHRONIZING` peut être attendu en mode asynchrone.
- `NOT_HEALTHY`, `DISCONNECTED` ou `is_suspended = 1` : comparer aux alertes et escalader.
- Zéro ligne peut signifier aucun AG configuré ou droits insuffisants.

**Droits DMV :** 2019 `VIEW SERVER STATE` ; 2022+ `VIEW SERVER PERFORMANCE STATE`.

**Escalade :** AG/réplica, état prévu/observé, heure, impact. Ne jamais basculer, reprendre ou suspendre la réplication en N1.

[Source : états AG](https://learn.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)
