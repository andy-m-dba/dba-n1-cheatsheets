# MYSQL-N1-04 — Réplication

**Quand ?** Réplica absent, retard, threads de réplication arrêtés.

### Sur un réplica MySQL 8.x (client mysql)
```sql
SHOW REPLICA STATUS\G
```

### Sur un réplica MariaDB (client mariadb)
```sql
SHOW SLAVE STATUS\G
-- Si multi-source : SHOW ALL SLAVES STATUS\G
```

### Lecture rapide
- MySQL : `Replica_IO_Running`, `Replica_SQL_Running`, `Seconds_Behind_Source`.
- MariaDB : `Slave_IO_Running`, `Slave_SQL_Running`, `Seconds_Behind_Master`.
- Une valeur `0` ou `NULL` pour le retard **ne suffit pas** à établir que tout est synchronisé.
- Pas de ligne : aucun canal retourné dans ce contexte, à comparer à l'architecture prévue.
- Droits : MySQL `REPLICATION CLIENT` ; MariaDB `REPLICA MONITOR` (selon version).

**Escalade :** canal, threads, lag, erreur expurgée, heure, impact. Aucun `STOP/START REPLICA` ni bascule N1.

[Sources : MySQL](https://dev.mysql.com/doc/refman/8.4/en/show-replica-status.html) · [MariaDB](https://mariadb.com/docs/server/reference/sql-statements/administrative-sql-statements/show/show-replica-status)
