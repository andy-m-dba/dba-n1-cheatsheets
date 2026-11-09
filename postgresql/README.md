# PostgreSQL — CheatSheets N1

**Public :** DBA N1 / exploitation  
**Statut :** Brouillon en attente de revue technique N2/N3  
**Versions cibles :** PostgreSQL 14 à 18 (fonctionnalités communes revues dans la documentation officielle). PostgreSQL 12/13 sont hors support. PostgreSQL 14 atteint sa fin de support le **12 novembre 2026** : préparer la montée de version avec N2/N3.  
**Environnement :** `psql`, `pg_isready`, commandes Linux si hôte autorisé.  
**Revue documentaire :** 2026-11-09 · **Exécution réelle :** non testée · **Validation par N2/N3 :** en attente.

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
- Certaines colonnes des vues statistiques sont masquées sans privilèges suffisants. Le rôle `pg_read_all_stats` peut être étudié par N2/N3 ; N1 ne s'accorde aucun privilège. L'absence de ligne ou une valeur `NULL` n'est pas toujours synonyme d'absence d'incident.
- Les statistiques cumulées peuvent être retardées ou mises en cache dans une transaction. Exécuter les relevés séparément, sans conserver une transaction de diagnostic ouverte ; comparer des mesures horodatées.
- Ne pas modifier les services, fichiers, paramètres, comptes ou sessions.
- Les seuils ne sont pas universels : toujours se référer au contrat local.

## Statut de validation

La [revue technique documentaire](REVUE-TECHNIQUE.md) indique les points contrôlés, les limites et les tests à conduire. Elle ne constitue **pas** une certification de fonctionnement sur PostgreSQL 14–18.

## Documentation

[Monitoring](https://www.postgresql.org/docs/current/monitoring.html) · [Vues de statistiques](https://www.postgresql.org/docs/current/monitoring-stats.html) · [psql](https://www.postgresql.org/docs/current/app-psql.html).
