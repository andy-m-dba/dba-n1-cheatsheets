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
WHERE backend_type = 'client backend'
GROUP BY datname, state
ORDER BY datname, nb DESC;
```

- `active` : requête en cours, pas nécessairement lente.
- `idle` : attend une nouvelle commande, souvent normal.
- `idle in transaction` : transaction ouverte mais sans requête active, à surveiller.
- `state = NULL` : certaines informations non exposées (droits insuffisants) ou collecte désactivée ; l'exemple compte les connexions clientes, pas les processus internes.
- `active` et `wait_event` décrivent deux dimensions différentes : une session active peut aussi être en attente.

## 2. Requêtes actives les plus anciennes (sans texte SQL)

```sql
SELECT pid, usename, datname, state,
       wait_event_type, wait_event,
       now() - query_start AS duree_requete
FROM pg_stat_activity
WHERE backend_type = 'client backend'
  AND state = 'active'
  AND pid <> pg_backend_pid()
ORDER BY query_start ASC NULLS LAST
LIMIT 20;
```

Une durée élevée n'établit pas à elle seule une anomalie.

## 3. Processus bloqués

```sql
WITH diagnostic AS MATERIALIZED (
  SELECT pid, datname, usename, wait_event_type, wait_event,
         pg_blocking_pids(pid) AS pids_bloqueurs
  FROM pg_stat_activity
  WHERE backend_type = 'client backend'
)
SELECT pid, datname, usename, wait_event_type, wait_event, pids_bloqueurs
FROM diagnostic
WHERE cardinality(pids_bloqueurs) > 0
ORDER BY pid;
```

Une vue vide indique l'absence de blocage visible au moment du relevé, **pas** l'absence de tout problème de performance. Les PID retournés peuvent être dupliqués avec le parallélisme ; `0` représente parfois une transaction préparée. La CTE `MATERIALIZED` (PostgreSQL 12+) évite le recalcul de `pg_blocking_pids()` pour une même session dans ce relevé. La fonction interroge le gestionnaire de verrous : **ne pas lancer ce relevé à haute fréquence**. Ne jamais interpréter des colonnes masquées comme des valeurs observées.

## Escalade

Consigner date, impact, base, nombre de sessions, durées observées et PID bloqués/bloqueurs dans un ticket interne. Escalader si impact ou seuil local dépassé.

**Interdit N1 autonome :** `pg_cancel_backend`, `pg_terminate_backend` ou tout changement de paramètre.

**Source :** [Statistiques PostgreSQL](https://www.postgresql.org/docs/current/monitoring-stats.html).
