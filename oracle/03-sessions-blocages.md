# ORA-N1-03 — Sessions & blocages

**Quand ?** Lenteur, utilisateurs en attente, session bloquée.

### Sessions utilisateur par statut
```sql
SELECT status, COUNT(*) AS nb
FROM v$session
WHERE type = 'USER'
GROUP BY status ORDER BY nb DESC;
```

### Sessions bloquées visibles
```sql
SELECT sid, serial#, status, event,
       blocking_instance, blocking_session
FROM v$session
WHERE blocking_session_status = 'VALID';
```

### Lecture rapide
- `ACTIVE` ≠ requête anormalement lente ; `INACTIVE` ≠ incident.
- `blocking_session` est un **SID** ; vérifier aussi `blocking_instance` en RAC.
- Une vue vide = aucun blocage identifié à cet instant ; le problème peut être transitoire.
- Visibilité soumise aux droits `V$SESSION`; accès refusé = escalade, pas élévation N1.

**Escalade :** heure, SID/SERIAL#, instance, attente et impact. Ne pas lancer `ALTER SYSTEM KILL SESSION`.

[Source : V$SESSION](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-SESSION.html)
