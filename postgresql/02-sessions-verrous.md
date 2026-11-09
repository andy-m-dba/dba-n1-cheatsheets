# PG-N1-02 — Sessions & verrous

**Quand ?** Lenteurs, transactions en attente, trop de sessions.

### Répartition des connexions clientes

```sql
SELECT state, count(*) AS nb
FROM pg_stat_activity
WHERE backend_type = 'client backend'
GROUP BY state ORDER BY nb DESC;
```

### Transactions ouvertes les plus anciennes

```sql
SELECT pid, datname, state, wait_event_type, wait_event,
       now() - xact_start AS age_transaction
FROM pg_stat_activity
WHERE backend_type = 'client backend' AND xact_start IS NOT NULL
ORDER BY xact_start LIMIT 10;
```

### Blocages visibles (requête ponctuelle)

```sql
SELECT pid, wait_event, pg_blocking_pids(pid) AS bloque_par
FROM pg_stat_activity
WHERE backend_type = 'client backend' AND wait_event_type = 'Lock';
```

### Lecture rapide

- `idle in transaction` : transaction ouverte inactive ; à signaler si durable.
- `Lock` : attente de verrou ; relever les PID (sans tuer de session).
- Résultat vide : rien de visible **à cet instant**. Certaines données sont masquées sans droits de supervision.
- Ne pas exécuter `pg_blocking_pids()` en boucle à haute fréquence.

**Escalade :** impact, heure, nombre de sessions, âge, PID bloqués. Ne jamais lancer `pg_cancel_backend` ou `pg_terminate_backend` en N1 sans procédure approuvée.

[Référence : pg_stat_activity](https://www.postgresql.org/docs/current/monitoring-stats.html)
