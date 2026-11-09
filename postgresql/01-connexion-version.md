# PG-N1-01 — Connexion & version

**Quand ?** Connexion refusée, timeout, doute sur le serveur ou le rôle.

### Commandes

```bash
pg_isready -h HOST -p 5432 -d DATABASE -U LECTURE
psql -X -h HOST -p 5432 -d DATABASE -U LECTURE
```

Dans `psql` (après connexion) :

```sql
SELECT current_database() AS base, current_user AS utilisateur,
       current_setting('server_version') AS version,
       pg_is_in_recovery() AS standby;
```

### Lecture rapide

| Observation | Vérifier / transmettre |
|---|---|
| `connection refused` | Hôte, port, service ; remonter sans redémarrer |
| `timeout` | Réseau, filtrage, service |
| `password authentication failed` | Authentification ; ne jamais exposer le mot de passe |
| `no pg_hba.conf entry` | Politique d'accès ; remonter au N2 |
| `standby = true` | Instance en recovery / standby |
| `standby = false` | Hors recovery ; confirmer la topologie HA dans l'inventaire |

**Escalade :** heure, erreur expurgée, cible logique, impact et résultat. Aucun changement `pg_hba.conf` ou rôle.

[Références : psql](https://www.postgresql.org/docs/current/app-psql.html) · [pg_isready](https://www.postgresql.org/docs/current/app-pg-isready.html)
