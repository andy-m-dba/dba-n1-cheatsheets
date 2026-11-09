# ORA-N1-04 — Tablespaces & FRA

**Quand ?** Alerte espace, tablespace pleine, FRA saturée.

### Utilisation des tablespaces (avec droits DBA)
```sql
SELECT tablespace_name, ROUND(used_percent, 1) AS pct_utilise
FROM dba_tablespace_usage_metrics
ORDER BY used_percent DESC;
```

### Fast Recovery Area (FRA)
```sql
SELECT ROUND(space_limit/1024/1024/1024,1) AS limite_go,
       ROUND(space_used/1024/1024/1024,1) AS utilise_go,
       ROUND(space_reclaimable/1024/1024/1024,1) AS recuperable_go
FROM v$recovery_file_dest;
```

### Lecture rapide
- `USED_PERCENT` tient compte de la taille potentielle et de certaines contraintes de stockage ; **ce n'est pas** le taux d'utilisation du disque OS.
- `SPACE_USED` peut inclure des fichiers d'anciennes FRA : comparer aux métriques de supervision.
- `SPACE_RECLAIMABLE` ne donne **pas** au N1 l'autorisation d'effacer des fichiers.
- Vue vide / `ORA-00942` : FRA non configurée, visibilité limitée ou privilèges insuffisants selon la vue.

**Escalade :** tablespace/FRA, seuil et tendance, impact. Jamais de `RESIZE`, `ADD DATAFILE` ou purge N1.

[Sources : tablespaces](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/DBA_TABLESPACE_USAGE_METRICS.html) · [FRA](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-RECOVERY_FILE_DEST.html)
