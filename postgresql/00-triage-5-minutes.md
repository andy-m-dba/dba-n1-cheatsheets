# PG-N1-00 — Runbook express : incident PostgreSQL (5 min)

**Quand ?** Alerte « base inaccessible », lenteurs ou statut inconnu.

### 1. Identifier l'impact (1 min)

Noter **heure + fuseau**, application, symptôme exact, utilisateurs affectés et alerte de supervision.

### 2. Tester la disponibilité (1 min)

```bash
pg_isready -h HOST -p 5432 -d DATABASE -U LECTURE
echo $?   # 0=accepte, 1=rejette, 2=pas de réponse, 3=paramètre invalide
```

`0` **n'atteste ni l'authentification ni la santé de l'application**.

### 3. Si l'accès SQL est possible (2 min)

```sql
SELECT now() AS heure, current_database() AS base,
       pg_is_in_recovery() AS standby,
       pg_postmaster_start_time() AS demarrage;

SELECT state, count(*) AS nb
FROM pg_stat_activity
WHERE backend_type = 'client backend'
GROUP BY state;
```

Pour approfondir : [connexion](01-connexion-version.md) · [sessions](02-sessions-verrous.md) · [disque](03-espace-capacite.md) · [réplication](04-replication.md) · [WAL](05-wal-sauvegardes.md).

### 4. Escalader et transmettre (1 min)

```text
Heure (TZ) : ...
Service / impact : ...
Alerte / erreur expurgée : ...
pg_isready : code ...
Accès SQL : OK / KO ; rôle : primaire / standby / inconnu
Constats et écarts avec l'état attendu : ...
Vérifications impossibles (droits, réseau) : ...
```

**Escalade immédiate** si indisponibilité métier, risque de perte de données ou stockage presque saturé selon les seuils internes. Pas de redémarrage, purge WAL, kill session ou failover par le N1.

[Référence : pg_isready](https://www.postgresql.org/docs/current/app-pg-isready.html)
