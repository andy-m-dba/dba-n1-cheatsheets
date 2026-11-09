# MYSQL-N1-04 — État de la réplication

**Quand ?** Réplica absent, retard ou canal arrêté.

### MySQL 8.0.22+ / 8.4 — sur le réplica, client mysql
```sql
SHOW REPLICA STATUS\G
```

### MariaDB 10.11 / 11.x — sur le réplica, client mariadb
```sql
SHOW SLAVE STATUS\G
-- Multi-source : SHOW ALL SLAVES STATUS\G
```

### Lecture rapide
- **MySQL** : `Replica_IO_Running`, `Replica_SQL_Running`, `Seconds_Behind_Source`.
- **MariaDB** : `Slave_IO_Running`, `Slave_SQL_Running`, `Seconds_Behind_Master`.
- `No` / `Connecting` sur un thread attendu : relever aussi `Last_IO_Error` et `Last_SQL_Error` **expurgés**.
- Retard `0` ou `NULL` : **pas** une preuve que toutes les données sont synchronisées.
- Aucune ligne : comparer aux canaux attendus. Droits usuels : MySQL `REPLICATION CLIENT`, MariaDB `REPLICA MONITOR`.

**Escalade :** canal, état des threads, retard, erreur expurgée et impact. Aucun `STOP/START REPLICA` ni bascule N1.

[Sources : MySQL](https://dev.mysql.com/doc/refman/8.4/en/show-replica-status.html) · [MariaDB](https://mariadb.com/docs/server/reference/sql-statements/administrative-sql-statements/show/show-replica-status)
