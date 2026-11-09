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

## À venir

`sqlserver/`, `oracle/`, `mongodb/` : même format court.

Documentation : [PostgreSQL](https://www.postgresql.org/docs/current/) · [Politique de versions](https://www.postgresql.org/support/versioning/)
