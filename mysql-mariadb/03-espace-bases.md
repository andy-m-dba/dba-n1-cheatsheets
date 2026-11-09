# MYSQL-N1-03 — Espace disque & bases

**Quand ?** Stockage presque plein ou croissance inhabituelle.

### Taille estimée des bases visibles
```sql
SELECT TABLE_SCHEMA AS base,
       ROUND(SUM(DATA_LENGTH + INDEX_LENGTH)/1024/1024, 1) AS taille_mio
FROM information_schema.TABLES
WHERE TABLE_SCHEMA NOT IN
  ('information_schema', 'performance_schema', 'mysql', 'sys')
GROUP BY TABLE_SCHEMA
ORDER BY taille_mio DESC;
```

### Volumes OS (hôte autorisé)
```bash
df -h
df -i
```

### Lecture rapide
- Pour InnoDB, la taille issue de `information_schema` est **estimée**.
- Elle n'inclut pas nécessairement binlogs, redo/undo, temporaires et backups.
- Les bases non visibles peuvent être masquées par les droits.
- `df` mesure les volumes : confirmer ceux des données et journaux dans l'inventaire.

**Escalade :** volume, occupation, tendance, base et impact. Aucune purge de binlogs, suppression ou optimisation N1.

[Source : INFORMATION_SCHEMA.TABLES](https://dev.mysql.com/doc/refman/8.4/en/information-schema-tables-table.html)
