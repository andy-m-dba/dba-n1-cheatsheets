# MYSQL-N1-05 — Sauvegardes

**Quand ?** Job en échec, sauvegarde attendue absente, risque RPO.

### Vérifier l'outil utilisé (lecture seule)
- `mysqldump` / `mariadb-dump` : ordonnanceur et statut des jobs.
- `mysqlbackup`, `mariadb-backup`, snapshots ou solution tierce : console de backup.
- Binlogs : vérifier la **politique** attendue, sans modifier la rétention.

### Lecture rapide
- Dernier job terminé ≠ preuve de sauvegarde **restaurable**.
- Snapshot présent ≠ vérification de cohérence ou de PITR.
- Absence de job dans l'ordonnanceur courant ≠ absence de toutes les sauvegardes.
- Comparer dernier succès et fréquence au RPO/RTO contractuels.

**Escalade :** base, outil, type, dernière réussite, statut, erreur expurgée. Aucun backup forcé, purge binlog ou restauration N1.

[Sources : MySQL Backup](https://dev.mysql.com/doc/refman/8.4/en/backup-and-recovery.html) · [MariaDB Backup](https://mariadb.com/docs/server/server-usage/backup-and-restore/)
