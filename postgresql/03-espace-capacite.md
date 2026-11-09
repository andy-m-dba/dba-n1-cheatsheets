# PG-N1-03 — Espace disque et capacité

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Symptômes

Alerte espace, croissance rapide, limite de connexions approchée, erreur de stockage.

## Prérequis

Lecture SQL autorisée et, pour les commandes Linux, accès au bon serveur explicitement approuvé.

## Taille des bases

```sql
SELECT datname, pg_size_pretty(pg_database_size(oid)) AS taille
FROM pg_database
WHERE datallowconn
ORDER BY pg_database_size(oid) DESC;
```

La fonction peut demander des privilèges supplémentaires pour certaines bases. Une taille SQL ne mesure pas l'espace libre du filesystem.

## Connexions

```sql
SELECT count(*) AS connexions_observees,
       current_setting('max_connections')::integer AS max_connections
FROM pg_stat_activity;
```

`max_connections` ne correspond pas exactement aux places ouvertes aux applications : réservations et contraintes additionnelles peuvent s'appliquer.

## Linux, uniquement avec autorisation

```bash
df -h
df -i
```

- `df -h` : occupation des volumes.
- `df -i` : occupation des inodes.
- Identifier les bons volumes (données, WAL, tablespaces, logs, backups) grâce à l'inventaire interne.

## Interprétation et escalade

Comparer les mesures à la supervision et aux seuils officiels. Relever la tendance avec au moins deux points horodatés. Si saturation avérée, escalader immédiatement selon criticité.

**Ne jamais** effacer `pg_wal`, journaux, sauvegardes ou fichiers PostgreSQL pour libérer de l'espace.

**Sources :** [Fonctions d'administration et taille](https://www.postgresql.org/docs/current/functions-admin.html) · [Monitoring](https://www.postgresql.org/docs/current/monitoring.html).
