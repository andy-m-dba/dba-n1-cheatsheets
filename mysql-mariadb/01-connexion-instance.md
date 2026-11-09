# MYSQL-N1-01 — Connexion & instance

**Quand ?** Accès refusé, timeout, doute sur le moteur ou le rôle.

### Connexion (client disponible)
```bash
mysql --host=HOST --port=3306 --user=LECTURE --password
# Sur MariaDB, utiliser aussi : mariadb --host=HOST --port=3306 --user=LECTURE --password
```

### Identification
```sql
SELECT VERSION() AS version, @@version_comment AS distribution,
       @@hostname AS node, @@port AS port, @@read_only AS lecture_seule;
SELECT CURRENT_USER() AS compte_authentifie, DATABASE() AS base;
```

### Lecture rapide
- `Access denied` : compte, hôte d'origine ou politique d'accès.
- `Can't connect` / timeout : réseau, port, processus ou TLS.
- `read_only = 1` **ne prouve pas** que le serveur soit un réplica ; vérifier l'architecture.
- Un port différent de `3306` est fréquent (multi-instances, proxy, cloud).

**Escalade :** heure, erreur expurgée, cible logique et impact. Ne modifier ni droits, ni paramètres.

[Sources : MySQL](https://dev.mysql.com/doc/refman/8.4/en/) · [MariaDB](https://mariadb.com/docs/server/)
