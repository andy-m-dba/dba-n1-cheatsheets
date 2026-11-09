# PG-N1-02 — Sessions et blocages

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Symptômes

Lenteurs, application figée, sessions en attente, connexions anormalement nombreuses.

## Prérequis et précautions

Accès SQL de lecture. Les colonnes des autres sessions peuvent être masquées selon les privilèges. Ne pas transmettre le texte SQL métier en dehors du canal interne autorisé.

## 1. Sessions par base et état

```sql
SELECT datname, state, count(*) AS nb
FROM pg_stat_activity
GROUP BY datname, state
ORDER BY datname, nb DESC;
```

- `active` : requête en cours, pas nécessairement lente.
- `idle` : attend une nouvelle commande, souvent normal.
- `idle in transaction` : transaction ouverte mais sans requête active, à surveiller.
- `state = NULL` : certaines sessions techniques ou informations non exposées.

## 2. Requêtes actives les plus anciennes (sans texte SQL)

```sql
SELECT pid, usename, datname, state,
       wait_event_type, wait_event,
       now() - query_start AS duree_requete
FROM pg_stat_activity
WHERE state = 'active'
  AND pid <> pg_backend_pid()
ORDER BY query_start ASC NULLS LAST
LIMIT 20;
```

Une durée élevée n'établit pas à elle seule une anomalie.

## 3. Processus bloqués

```sql
SELECT pid, datname, usename, wait_event_type, wait_event,
       pg_blocking_pids(pid) AS pids_bloqueurs
FROM pg_stat_activity
WHERE cardinality(pg_blocking_pids(pid)) > 0
ORDER BY pid;
```

Une vue vide indique l'absence de blocage visible au moment du relevé, **pas** l'absence de tout problème de performance.

## Escalade

Consigner date, impact, base, nombre de sessions, durées observées et PID bloqués/bloqueurs dans un ticket interne. Escalader si impact ou seuil local dépassé.

**Interdit N1 autonome :** `pg_cancel_backend`, `pg_terminate_backend` ou tout changement de paramètre.

**Source :** [Statistiques PostgreSQL](https://www.postgresql.org/docs/current/monitoring-stats.html).
