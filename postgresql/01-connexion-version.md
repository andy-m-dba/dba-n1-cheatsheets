# PG-N1-01 — Connexion et identification

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Symptômes

Connexion refusée, timeout, échec d'authentification, doute sur le rôle du serveur.

## Prérequis

Poste, réseau et compte autorisés ; `psql` et `pg_isready` installés. Ne jamais ajouter de mot de passe à une ligne de commande ou au dépôt.

## Vérifications

```bash
pg_isready -h HOTE_EXEMPLE -p 5432 -d BASE_EXEMPLE -U UTILISATEUR_LECTURE
psql -X -h HOTE_EXEMPLE -p 5432 -d BASE_EXEMPLE -U UTILISATEUR_LECTURE
```

Dans `psql` :

```text
\conninfo
```

```sql
SELECT current_database() AS base,
       current_user AS utilisateur,
       inet_server_addr() AS adresse_serveur,
       inet_server_port() AS port,
       current_setting('server_version') AS version_serveur,
       pg_is_in_recovery() AS est_standby;
```

- `est_standby = true` : instance en recovery/standby.
- `false` : hors recovery, normalement primaire selon l'architecture.
- `inet_server_addr()` peut valoir `NULL` via socket Unix.
- Version `psql` et version serveur ne sont pas nécessairement identiques.
- `pg_is_in_recovery() = false` ne garantit pas que ce serveur soit le bon primaire pour l'application : vérifier l'inventaire et l'orchestrateur HA éventuel.
- Ne publier ni la sortie brute de `\conninfo` ni les adresses renvoyées dans un dépôt GitHub.

## Erreurs courantes

| Message | Piste possible, non confirmée |
|---|---|
| `connection refused` | Service non à l'écoute ou hôte/port erroné |
| `timeout` | Réseau, filtrage ou service |
| `password authentication failed` | Identifiants ou politique d'authentification |
| `no pg_hba.conf entry` | Règle d'accès non applicable |
| `database ... does not exist` | Cible erronée |

**Escalade :** transmettre erreur expurgée, heure, adresse logique ciblée via ticket interne et impact. Ne modifier ni `pg_hba.conf` ni les comptes.

**Sources :** [psql](https://www.postgresql.org/docs/current/app-psql.html) · [pg_isready](https://www.postgresql.org/docs/current/app-pg-isready.html).
