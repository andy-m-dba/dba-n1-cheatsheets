# MYSQL-N1-01 — Connexion & identification

**Quand ?** Accès refusé, timeout, instance ou rôle incertain.

### Se connecter
```bash
mysql -h HOST -P 3306 -u LECTURE --password
# MariaDB : remplacer mysql par mariadb.
```
Adapter port, TLS et compte à l'inventaire. Saisir le mot de passe **à l'invite**.

### Identifier
```sql
SELECT VERSION() AS version, @@version_comment AS distribution,
       @@hostname AS hote, @@port AS port,
       @@read_only AS lecture_seule;
SELECT CURRENT_USER() AS compte_authentifie, DATABASE() AS base;
```

### Lecture rapide
- `Access denied` : compte, hôte d'origine ou règle d'accès.
- `Can't connect` / timeout : réseau, service, port ou TLS.
- `read_only = 1` ne prouve **pas** que l'instance est un réplica.
- `3306` est un exemple : utiliser le port réellement configuré.

**Escalade :** heure, cible logique, erreur expurgée et impact. Ne changer ni comptes, ni service, ni paramètres.

[Sources : MySQL](https://dev.mysql.com/doc/refman/8.4/en/) · [MariaDB](https://mariadb.com/docs/server/)
