# DBA N1 — CheatSheets

**But :** trouver une commande de diagnostic en moins d'une minute. Une fiche = un problème, des commandes et une règle d'escalade.

**Périmètre N1 :** observer, qualifier, transmettre. Toutes les commandes doivent être exécutées avec un accès **autorisé**, de préférence en lecture seule. **Ne pas** redémarrer, modifier la configuration, tuer des sessions ou supprimer des fichiers.

## PostgreSQL

| Situation | Fiche |
|---|---|
| Incident en cours / premier diagnostic | [00 — Runbook express (5 min)](postgresql/00-triage-5-minutes.md) |
| Connexion impossible / version | [01 — Connexion & instance](postgresql/01-connexion-version.md) |
| Lenteur / blocage / sessions | [02 — Sessions & verrous](postgresql/02-sessions-verrous.md) |
| Disque plein / connexions | [03 — Espace & capacité](postgresql/03-espace-capacite.md) |
| Réplication / standby | [04 — Réplication](postgresql/04-replication.md) |
| WAL / sauvegarde | [05 — WAL & backups](postgresql/05-wal-sauvegardes.md) |

**Utilisation :** adapter `HOST`, `DATABASE` et `LECTURE` aux valeurs de l'inventaire interne. Ne jamais copier de mot de passe ou de sortie sensible sur GitHub. Un résultat vide, `NULL` ou un accès refusé ne prouve pas qu'il n'y a pas d'incident.

**Versions visées :** PostgreSQL 14 à 18 ; vérifier la compatibilité avec la version réellement exploitée. Exemples documentaires, non exécutés sur une instance de test.

## SQL Server

| Situation | Fiche |
|---|---|
| Incident en cours | [00 — Runbook express](sqlserver/00-triage-5-minutes.md) |
| Connexion impossible / version | [01 — Connexion & instance](sqlserver/01-connexion-instance.md) |
| Base indisponible | [02 — État des bases](sqlserver/02-etat-bases.md) |
| Lenteur / sessions / blocages | [03 — Sessions & blocages](sqlserver/03-sessions-blocages.md) |
| Stockage / fichiers | [04 — Espace & fichiers](sqlserver/04-espace-fichiers.md) |
| Backup / RPO | [05 — Sauvegardes](sqlserver/05-sauvegardes.md) |
| Réplication / AG | [06 — Always On](sqlserver/06-always-on.md) |

**Versions visées :** SQL Server 2019, 2022, 2025 (instances classiques ; Azure SQL Database a des droits et vues différents). Les exemples ne sont pas exécutés sur une instance de test.

## Oracle

| Situation | Fiche |
|---|---|
| Incident / ORA-xxxxx | [00 — Runbook express](oracle/00-triage-5-minutes.md) |
| Connexion / instance | [01 — Connexion & rôle](oracle/01-connexion-instance.md) |
| PDB inaccessible | [02 — État des PDB](oracle/02-etat-pdb.md) |
| Lenteurs / verrous | [03 — Sessions & blocages](oracle/03-sessions-blocages.md) |
| Stockage / FRA | [04 — Tablespaces & FRA](oracle/04-tablespaces-fra.md) |
| Sauvegardes | [05 — RMAN](oracle/05-sauvegardes.md) |
| Réplication | [06 — Data Guard](oracle/06-data-guard.md) |
| Erreurs récentes | [07 — Alert log](oracle/07-alert-log.md) |

**Cible :** Oracle Database 19c et versions récentes compatibles ; adapter à l'architecture CDB/PDB, RAC, Data Guard et aux privilèges réels. Exemples non testés en instance.

## MongoDB

| Situation | Fiche |
|---|---|
| Incident / alerte | [00 — Runbook express](mongodb/00-triage-5-minutes.md) |
| Connexion / version / rôle | [01 — Connexion & version](mongodb/01-connexion-version.md) |
| Base ou collection inaccessible | [02 — Bases & collections](mongodb/02-bases-collections.md) |
| Lenteurs / connexions | [03 — Opérations & connexions](mongodb/03-operations-connexions.md) |
| Stockage / disque | [04 — Espace & stockage](mongodb/04-espace-stockage.md) |
| Replica set | [05 — Réplication](mongodb/05-replication.md) |
| Backup / RPO | [06 — Sauvegardes](mongodb/06-sauvegardes.md) |
| Erreurs récentes | [07 — Logs](mongodb/07-logs.md) |

**Versions visées :** MongoDB 7.0–8.x ; certaines commandes de supervision exigent des droits supplémentaires et ne sont pas proposées sur toutes les offres Atlas. Exemples non exécutés sur serveur de test.

## MySQL / MariaDB

| Situation | Fiche |
|---|---|
| Incident | [00 — Runbook express](mysql-mariadb/00-triage-5-minutes.md) |
| Connexion | [01 — Connexion & instance](mysql-mariadb/01-connexion-instance.md) |
| Lenteurs | [02 — Sessions & connexions](mysql-mariadb/02-sessions-connexions.md) |
| Disque | [03 — Espace & tailles](mysql-mariadb/03-espace-bases.md) |
| Réplication | [04 — Réplication](mysql-mariadb/04-replication.md) |
| Backup | [05 — Sauvegardes](mysql-mariadb/05-sauvegardes.md) |
| Alertes | [06 — Erreurs & logs](mysql-mariadb/06-erreurs-logs.md) |

**Cible :** MySQL 8.0/8.4 et MariaDB 10.11/11.x, avec commandes de réplication distinctes. Exemples non exécutés en laboratoire.

## Redis

| Situation | Fiche |
|---|---|
| Incident | [00 — Runbook express](redis/00-triage-5-minutes.md) |
| Connexion | [01 — Connexion & version](redis/01-connexion-version.md) |
| Mémoire | [02 — Mémoire & évictions](redis/02-memoire-evictions.md) |
| Connexions / ralentissement | [03 — Clients & latence](redis/03-clients-latence.md) |
| Cluster / réplication | [04 — Réplication & cluster](redis/04-replication-cluster.md) |
| Backups | [05 — Persistance](redis/05-persistance-backups.md) |
| Alertes | [06 — Erreurs & stats](redis/06-erreurs-stats.md) |

**Cible :** Redis Open Source 7.x–8.x, à adapter à l'offre managée, TLS et ACL. Exemples non exécutés sur serveur de test.

## Cassandra

| Situation | Fiche |
|---|---|
| Incident | [00 — Runbook express](cassandra/00-triage-5-minutes.md) |
| Connexion / version | [01 — Connexion & version](cassandra/01-connexion-version.md) |
| État du ring | [02 — État du cluster](cassandra/02-etat-cluster.md) |
| Lenteurs / files | [03 — Threads & activité](cassandra/03-threads-activite.md) |
| Disque | [04 — Stockage & tables](cassandra/04-stockage.md) |
| Compactions | [05 — Compactions & streaming](cassandra/05-compactions-streaming.md) |
| Backup | [06 — Sauvegardes](cassandra/06-sauvegardes.md) |
| Incidents | [07 — Logs](cassandra/07-logs.md) |

**Cible :** Apache Cassandra 4.1/5.0. `nodetool` requiert un accès JMX autorisé, distinct de CQL. Exemples non exécutés en laboratoire.

**Principe pour les cheatsheets et futurs labs :** un objectif concret, commandes reproductibles, lecture rapide du résultat ; un runbook seulement si utile, aucun fichier superflu.

Documentation : [PostgreSQL](https://www.postgresql.org/docs/current/) · [SQL Server](https://learn.microsoft.com/en-us/sql/sql-server/) · [Oracle Database](https://docs.oracle.com/en/database/oracle/oracle-database/19/) · [MongoDB](https://www.mongodb.com/docs/manual/)
