# MSSQL-N1-05 — Sauvegardes

**Quand ?** Job backup en échec, sauvegarde récente absente, alerte RPO.

### Historique local (si accès autorisé à msdb)
```sql
SELECT TOP (20) database_name, type,
       backup_start_date, backup_finish_date
FROM msdb.dbo.backupset
ORDER BY backup_finish_date DESC;
```

### Lecture rapide
- `D` = Full, `I` = Differential, `L` = Transaction log.
- Comparer la fréquence **par base** au plan de sauvegarde attendu.
- Pas de ligne ≠ aucune sauvegarde : historique `msdb` purgé, outils externes, droits limités.
- Historique présent ≠ preuve de restauration réussie.

Vérifier les jobs dans **SQL Server Agent** ou l'outil de sauvegarde de l'organisation (lecture seule).

**Escalade :** base, dernier succès attendu/observé, statut du job, erreur expurgée, objectif RPO. Ne pas lancer de `BACKUP`/`RESTORE` N1 sans procédure approuvée.

[Source : msdb.dbo.backupset](https://learn.microsoft.com/en-us/sql/relational-databases/system-tables/backupset-transact-sql)
