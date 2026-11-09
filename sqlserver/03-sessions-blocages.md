# MSSQL-N1-03 — Sessions & blocages

**Quand ?** Lenteur, requêtes bloquées, connexions nombreuses.

### Sessions clientes par état
```sql
SELECT status, COUNT(*) AS sessions
FROM sys.dm_exec_sessions
WHERE is_user_process = 1
GROUP BY status ORDER BY sessions DESC;
```

### Requêtes bloquées / en attente
```sql
SELECT session_id, blocking_session_id, status,
       wait_type, wait_time AS wait_ms,
       total_elapsed_time AS elapsed_ms
FROM sys.dm_exec_requests
WHERE session_id <> @@SPID
  AND (blocking_session_id <> 0 OR wait_type IS NOT NULL)
ORDER BY total_elapsed_time DESC;
```

### Lecture rapide
- `blocking_session_id > 0` : SPID bloquant à signaler.
- `-2` à `-5` : cas spéciaux ; **pas** un SPID ordinaire.
- `wait_type` seul ≠ blocage anormal ; une attente peut être normale.
- Absence de lignes ≠ absence de problème. Sans droits DMV, la vue est partielle.

**Droits :** SQL Server 2019 : `VIEW SERVER STATE` ; 2022+ : `VIEW SERVER PERFORMANCE STATE`, à demander via N2.

**Escalade :** heure, SPID, attente, durée et impact. Jamais de `KILL` N1.

[Sources : sessions](https://learn.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) · [requêtes](https://learn.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql)
