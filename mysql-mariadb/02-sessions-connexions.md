# MYSQL-N1-02 — Sessions & connexions

**Quand ?** Trop de connexions, requêtes bloquées ou lentes.

### Compteurs globaux
```sql
SHOW GLOBAL STATUS WHERE Variable_name IN
('Threads_connected','Threads_running','Max_used_connections');
SHOW GLOBAL VARIABLES LIKE 'max_connections';
```

### Processus en cours (sans texte SQL)
```sql
SELECT ID, USER, DB, COMMAND, TIME, STATE
FROM information_schema.PROCESSLIST
WHERE COMMAND <> 'Sleep'
ORDER BY TIME DESC LIMIT 10;
```

### Lecture rapide
- `Threads_connected` = connexions ouvertes ; `Threads_running` = threads non endormis.
- `TIME` = durée de l'état courant, **pas forcément** durée d'une transaction.
- Sans privilège `PROCESS`, autres sessions invisibles. `INFORMATION_SCHEMA.PROCESSLIST` est dépréciée côté MySQL : adapter avec N2 si retirée.
- Comparer plusieurs relevés à la supervision ; aucune valeur isolée ne prouve un blocage.

**Escalade :** compteur, ID de connexion, état, durée, impact. Aucun `KILL` N1.

[Sources : MySQL PROCESSLIST](https://dev.mysql.com/doc/refman/8.4/en/show-processlist.html) · [MariaDB STATUS](https://mariadb.com/docs/server/reference/sql-statements/administrative-sql-statements/show/show-status)
