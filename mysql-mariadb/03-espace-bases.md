# MYSQL-N1-03 — Espace & tailles

**Quand ?** Alerte disque, croissance anormale, partition presque pleine.

### Taille approximative des bases visibles
```sql
SELECT TABLE_SCHEMA AS base,
  ROUND(SUM(DATA_LENGTH + INDEX_LENGTH)/1024/1024,1) AS taille_mio
FROM information_schema.TABLES
WHERE TABLE_SCHEMA NOT IN
 ('information_schema','performance_schema','mysql','sys')
GROUP BY TABLE_SCHEMA ORDER BY taille_mio DESC;
```

### Disque Linux (hôte autorisé)
```bash
df -h
df -i
```

### Lecture rapide
- `DATA_LENGTH` / `INDEX_LENGTH` sont des **estimations** pour InnoDB.
- Le total SQL ne couvre pas nécessairement binlogs, redo/undo, fichiers temporaires, backups ou disques du cluster.
- Une base absente peut être masquée par les droits.
- Comparer au taux réel du volume et à la tendance dans la supervision.

**Escalade :** base/volume, occupation, tendance et impact. Aucun `OPTIMIZE`, `PURGE BINARY LOGS` ou suppression manuelle N1.

[Source : INFORMATION_SCHEMA.TABLES](https://dev.mysql.com/doc/refman/8.4/en/information-schema-tables-table.html)
