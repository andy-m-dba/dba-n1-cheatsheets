# PostgreSQL — CheatSheets N1

**Public :** DBA N1 / exploitation  
**Statut :** Brouillon en attente de revue technique N2/N3  
**Versions :** SQL écrit pour PostgreSQL 12+ ; vérifier les différences et la prise en charge effective de la version installée.  
**Environnement :** `psql`, `pg_isready`, commandes Linux si hôte autorisé.  
**Vérification documentaire :** 2026-11-09 · **Test réel :** non effectué.

## Index

| ID | Fiche | Quand l'utiliser |
|---|---|---|
| PG-N1-00 | [Triage initial](00-triage-5-minutes.md) | Premier diagnostic en cinq minutes |
| PG-N1-01 | [Connexion et version](01-connexion-version.md) | Connexion refusée / instance inconnue |
| PG-N1-02 | [Sessions et blocages](02-sessions-verrous.md) | Lenteur / attente / nombre de connexions |
| PG-N1-03 | [Espace et capacité](03-espace-capacite.md) | Saturation / croissance / connexions |
| PG-N1-04 | [Réplication](04-replication.md) | Standby absent / réplication en retard |
| PG-N1-05 | [WAL et sauvegardes](05-wal-sauvegardes.md) | Archivage / jobs de backup |
| PG-N1-06 | [Escalade](06-escalade.md) | Transmettre un incident au N2/N3 |

## Accès et limites

- Toutes les commandes nécessitent un environnement autorisé ; utiliser un compte de lecture.
- Certaines colonnes des vues statistiques sont masquées sans privilèges suffisants. Le rôle `pg_read_all_stats` peut être demandé au N2/N3, jamais accordé par le N1.
- Ne pas modifier les services, fichiers, paramètres, comptes ou sessions.
- Les seuils ne sont pas universels : toujours se référer au contrat local.

## Documentation

[Monitoring](https://www.postgresql.org/docs/current/monitoring.html) · [Vues de statistiques](https://www.postgresql.org/docs/current/monitoring-stats.html) · [psql](https://www.postgresql.org/docs/current/app-psql.html).
