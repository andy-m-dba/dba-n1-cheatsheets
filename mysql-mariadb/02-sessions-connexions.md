# MYSQL-N1-02 — Sessions & connexions

**Quand ?** Connexions nombreuses, requêtes lentes ou blocages suspectés.

### Compteurs (MySQL et MariaDB)
```sql
SHOW GLOBAL STATUS WHERE Variable_name IN
  ('Threads_connected', 'Threads_running', 'Max_used_connections');
SHOW GLOBAL VARIABLES LIKE 'max_connections';
```

### Activité — MySQL 8.x (Performance Schema actif)
```sql
SELECT ID, USER, DB, COMMAND, TIME, STATE
FROM performance_schema.processlist
WHERE COMMAND <> 'Sleep'
ORDER BY TIME DESC LIMIT 10;
```

### Activité — MariaDB
```sql
SELECT ID, USER, DB, COMMAND, TIME, STATE
FROM information_schema.PROCESSLIST
WHERE COMMAND <> 'Sleep'
ORDER BY TIME DESC LIMIT 10;
```

### Lecture rapide
- `Threads_connected` : connexions ouvertes ; `Threads_running` : threads non endormis.
- `TIME` : durée en secondes de l'état actuel, **pas** forcément d'une transaction.
- Sans privilèges appropriés (`PROCESS` notamment), visibilité partielle ; une vue vide ne prouve rien.
- Comparer les compteurs à la supervision et à un relevé précédent.

**Escalade :** heure, compteurs, ID, état, durée et impact. Aucun `KILL` N1.

[Sources : MySQL Performance Schema](https://dev.mysql.com/doc/refman/8.4/en/performance-schema-processlist-table.html) · [MariaDB PROCESSLIST](https://mariadb.com/docs/server/reference/system-tables/information-schema/information-schema-tables/information-schema-processlist-table)
