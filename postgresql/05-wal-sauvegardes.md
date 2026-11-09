# PG-N1-05 — Archivage WAL et sauvegardes

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Symptômes

Alerte archivage WAL, job de sauvegarde en échec, rétention ou restauration incertaine.

## Archivage WAL

```sql
SHOW archive_mode;

SELECT archived_count, last_archived_wal, last_archived_time,
       failed_count, last_failed_wal, last_failed_time, stats_reset
FROM pg_stat_archiver;
```

- `archive_mode=off` peut être normal selon l'architecture.
- `failed_count` est cumulatif depuis `stats_reset`. Une valeur non nulle ne prouve pas un échec en cours ; des échecs provoquant le redémarrage de l'archiver peuvent aussi ne pas être comptabilisés. Corréler avec l'outil de supervision et les journaux expurgés.
- Comparer deux relevés horodatés ainsi que l'état de la solution de sauvegarde.
- Une date d'archivage ancienne peut être normale lorsqu'aucun WAL récent n'est prêt à archiver. Un `last_archived_wal` récent ne prouve pas que tous les WAL antérieurs ont été archivés.
- `archive_mode` actif ne prouve pas qu'une destination d'archivage soit correctement configurée ni que la politique de récupération soit satisfaite.
- Archivage réussi ≠ sauvegarde restaurable.

## Sauvegardes

Il n'existe pas de vue PostgreSQL universelle prouvant la réussite d'un outil externe comme pgBackRest, Barman ou des snapshots.

Dans l'outil autorisé, relever : nom du job, statut, dernière sauvegarde réussie, durée, stratégie de rétention et dernier test de restauration officiellement confirmé.

Ne jamais déclarer une sauvegarde restaurable sur la base du seul statut `success`.

## Escalade

Job attendu en échec, délai de sauvegarde hors objectifs locaux, compteur d'échecs qui augmente, stockage WAL menacé : transmettre immédiatement selon criticité.

**Interdits :** purge WAL, changement de `archive_command`, suppression de sauvegarde, tentative de restauration autonome.

**Sources :** [Statistiques de l'archivage](https://www.postgresql.org/docs/18/monitoring-stats.html) · [Archivage continu et PITR](https://www.postgresql.org/docs/18/continuous-archiving.html).
