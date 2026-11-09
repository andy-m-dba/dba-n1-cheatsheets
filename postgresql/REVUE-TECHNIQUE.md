# Revue technique documentaire — PostgreSQL N1

**Date :** 2026-11-09  
**Périmètre :** PostgreSQL 14–18 (vérifications documentaires et cohérence de procédures).  
**Statut :** Revue documentaire effectuée ; **tests SQL non exécutés**, **relecture N2/N3 en attente**.  
**Ne pas déduire** que ces commandes ont été validées en environnement de production.

## Vérifications réalisées

| Fiche | Point revu | Résultat |
|---|---|---|
| PG-N1-00 | Codes retour de `pg_isready` ; pas de garantie d'authentification | Documenté |
| PG-N1-01 | `psql`, identification SQL, rôle primaire/standby | Limites de découverte HA explicitées |
| PG-N1-02 | `pg_stat_activity`, `pg_blocking_pids` | Périmètre sessions clientes, privilèges et coût de collecte précisés |
| PG-N1-03 | `pg_database_size`, espace libre OS, limites de connexions | Filtre des bases accessibles et mesure partielle explicités |
| PG-N1-04 | `pg_stat_replication`, `pg_stat_wal_receiver`, date de replay | Valeurs NULL et faux diagnostic de retard précisés |
| PG-N1-05 | `pg_stat_archiver`, sauvegardes externes | Échecs non comptabilisés et preuve de restaurabilité distingués |
| PG-N1-06 | Matrice d'escalade, qualification / ticket | Limites de diagnostic ajoutées |

## Actions de test à planifier en laboratoire

À exécuter par un DBA autorisé, sur des environnements de test représentatifs :

- [ ] PostgreSQL 14, 15, 16, 17, 18 : ouvrir chaque fiche et exécuter ses commandes `SELECT` et `SHOW` sur une instance de laboratoire.
- [ ] Vérifier le rendu avec un rôle de lecture ordinaire et un rôle de supervision **préconfiguré par N2/N3** (sans élévation par N1).
- [ ] Comparer `pg_isready` à une connexion `psql` valide et à des cas de connexion refusée.
- [ ] Observer les sessions actives, les attentes et un verrou bloquant créé **uniquement en laboratoire** ; mesurer l'impact du relevé.
- [ ] Comparer les tailles SQL, `df -h` et `df -i` ; confirmer l'inventaire des volumes.
- [ ] Contrôler un primaire et un standby de test, y compris l'absence d'activité WAL.
- [ ] Comparer les statistiques d'archivage à un outil de sauvegarde de laboratoire et à un test de restauration validé.
- [ ] Faire relire la fiche d'escalade par l'équipe d'exploitation.

Ces tests ne sont pas encore réalisés. Aucun résultat de test n'est inventé.

## Points hors périmètre

Procédures de failover, `pg_hba.conf`, rotation de mots de passe, purge WAL, terminaison de sessions, correction de configuration, restauration : N2/N3 selon procédure autorisée.

## Sources officielles consultées

- [Politique de version PostgreSQL](https://www.postgresql.org/support/versioning/)
- [pg_isready](https://www.postgresql.org/docs/18/app-pg-isready.html)
- [psql](https://www.postgresql.org/docs/18/app-psql.html)
- [Vues de statistiques et privilèges](https://www.postgresql.org/docs/18/monitoring-stats.html)
- [Fonctions d'information dont pg_blocking_pids](https://www.postgresql.org/docs/18/functions-info.html)
- [Fonctions de taille](https://www.postgresql.org/docs/18/functions-admin.html)
- [Connexions et réserves](https://www.postgresql.org/docs/18/runtime-config-connection.html)
- [Archivage continu et PITR](https://www.postgresql.org/docs/18/continuous-archiving.html)
- [Rôles prédéfinis de supervision](https://www.postgresql.org/docs/18/predefined-roles.html)

Cette revue vérifie les références documentaires principalement sur PostgreSQL 18 et les colonnes utilisées dans la documentation PostgreSQL 14 ; la matrice d'essais multi-versions reste nécessaire.
