# ORA-N1-06 — Data Guard

**Quand ?** Alerte standby, transport ou apply lag.

### Rôle de la base
```sql
SELECT database_role, open_mode FROM v$database;
```

### Sur la standby : retard transport / apply
```sql
SELECT name, value, datum_time
FROM v$dataguard_stats
WHERE name IN ('transport lag', 'apply lag');
```

### Sur la primaire : destinations configurées
```sql
SELECT dest_id, status, error
FROM v$archive_dest
WHERE status NOT IN ('INACTIVE');
```

### Lecture rapide
- Aucun résultat dans `V$DATAGUARD_STATS` sur la primaire : **normal**.
- Si `DATUM_TIME` ne progresse plus entre deux relevés, la métrique de lag peut être obsolète.
- `ERROR` / `FULL` sur une destination attendue : anomalie à escalader.
- Un lag non nul se compare au seuil défini ; ne pas conclure sur un seul relevé.

**Escalade :** rôle, destination, lag, heure, état attendu. Pas de switchover/failover N1.

[Sources : Data Guard](https://docs.oracle.com/en/database/oracle/oracle-database/19/sbydb/oracle-data-guard-in-oracle-database-views.html) · [V$ARCHIVE_DEST](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-ARCHIVE_DEST.html)
