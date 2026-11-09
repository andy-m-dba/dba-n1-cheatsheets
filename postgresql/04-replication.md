# PG-N1-04 — Rôle et réplication physique

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Symptômes

Réplica absent, standby en retard, alerte WAL receiver ou doute sur le rôle d'un nœud.

**Périmètre :** réplication physique native. Patroni, repmgr et services managés nécessitent un runbook complémentaire adapté.

## Identifier le rôle

```sql
SELECT pg_is_in_recovery() AS est_standby;
```

`true` : recovery / standby. `false` : hors recovery, généralement primaire.

## Sur un primaire : réplicas connectés

```sql
SELECT application_name, client_addr, state, sync_state,
       write_lag, flush_lag, replay_lag
FROM pg_stat_replication
ORDER BY application_name;
```

- `streaming` : WAL sender en flux, sans preuve suffisante que le standby soit à jour. La vue peut aussi exposer un WAL sender associé à la réplication logique : consulter l'inventaire de l'architecture.
- Résultat vide : aucun WAL sender visible maintenant ; anomalie uniquement si un replica était attendu.
- `write_lag`, `flush_lag` et `replay_lag` peuvent être `NULL` avec un réplica à jour ou système inactif. Ces durées ne sont pas des prévisions de rattrapage.

## Sur un standby : WAL receiver

```sql
SELECT status, sender_host, last_msg_receipt_time,
       latest_end_lsn, latest_end_time
FROM pg_stat_wal_receiver;
```

Une vue vide doit être comparée à l'architecture prévue, notamment archivage WAL versus streaming.

## Dernier commit rejoué sur standby

```sql
SELECT pg_last_xact_replay_timestamp() AS dernier_commit_rejoue,
       now() - pg_last_xact_replay_timestamp() AS age_dernier_commit;
```

Exécuter cette requête **uniquement sur un standby**. Une durée élevée peut simplement signaler l'absence d'écritures sur le primaire : **ce n'est pas une mesure fiable du retard de réplication**. `NULL` est possible si aucun commit n'a été rejoué. Comparer aux alertes et métriques de l'outil de supervision.

## Escalade

Réplica attendu absent, retard dépassant le seuil local ou indisponibilité : transmettre état observé et alerte à N2/N3. Ne pas promouvoir de standby et ne pas déclencher de failover.

**Source :** [Vues de monitoring](https://www.postgresql.org/docs/current/monitoring-stats.html).
