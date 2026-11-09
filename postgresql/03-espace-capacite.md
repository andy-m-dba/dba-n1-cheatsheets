# PG-N1-03 — Espace disque & capacité

**Quand ?** Alerte stockage, croissance de base ou connexions saturées.

### Taille de la base connectée

```sql
SELECT current_database() AS base,
       pg_size_pretty(pg_database_size(current_database())) AS taille;
```

### Connexions

```sql
SELECT count(*) AS connexions_observees FROM pg_stat_activity;
SHOW max_connections;
```

### Espace OS (sur le serveur autorisé)

```bash
df -h   # blocs : espace libre et utilisé
df -i   # inodes : attention à la saturation
```

### Lecture rapide

- La taille SQL **n'est pas** l'espace libre du volume.
- Vérifier les volumes associés aux données, WAL et sauvegardes dans l'inventaire.
- `max_connections` n'égale pas le nombre de places ouvertes à l'application (connexions réservées).
- Comparer aux seuils locaux et à une mesure antérieure.

**Escalade :** volume, occupation, tendance, impact. Ne jamais supprimer de WAL, logs, backups ou fichiers du data directory.

[Références : fonctions de taille](https://www.postgresql.org/docs/current/functions-admin.html) · [monitoring](https://www.postgresql.org/docs/current/monitoring.html)
