# ORA-N1-05 — Sauvegardes RMAN

**Quand ?** Job échoué, dernier backup inconnu, alerte RPO.

### Derniers jobs RMAN (si accès autorisé)
```sql
SELECT input_type, status, start_time, end_time
FROM v$rman_backup_job_details
ORDER BY start_time DESC
FETCH FIRST 10 ROWS ONLY;
```

### Lecture rapide
- `COMPLETED` = job terminé ; **pas une preuve de restaurabilité**.
- `FAILED` ou `COMPLETED WITH ERRORS` = vérifier la stratégie et escalader.
- Distinguer `DB FULL`, `DB INCR`, `ARCHIVELOG` selon les objectifs.
- Historique absent ≠ absence de sauvegarde (rétention des métadonnées, recovery catalog, outil tiers).
- Comparer avec l'ordonnanceur / outil de sauvegarde validé.

**Escalade :** base, type, dernier succès attendu/observé, erreur expurgée, RPO. Aucun `BACKUP`, `DELETE` ou `RESTORE` N1.

[Source : V$RMAN_BACKUP_JOB_DETAILS](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-RMAN_BACKUP_JOB_DETAILS.html)
