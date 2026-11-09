# MYSQL-N1-00 — Runbook express (5 min)

**Quand ?** Connexion impossible, lenteur ou alerte MySQL/MariaDB.

### 1. Identifier (1 min)
Heure et fuseau, instance, application, erreur expurgée, impact.

### 2. Tester la connexion (1 min)
```bash
mysql -h HOST -P 3306 -u LECTURE --password -e "SELECT 1;"
# MariaDB : remplacer mysql par mariadb.
```
Port, TLS et compte : utiliser l'inventaire. Mot de passe **à l'invite**, jamais en argument.

### 3. Vérifier l'instance (2 min)
```sql
SELECT VERSION() AS version, @@read_only AS lecture_seule;
SHOW GLOBAL STATUS WHERE Variable_name IN
  ('Threads_connected', 'Threads_running', 'Aborted_connects');
```
Connexion SQL réussie ≠ application opérationnelle. `read_only = 1` ≠ preuve de réplication.

### 4. Orienter et escalader (1 min)
[Connexion](01-connexion-instance.md) · [Sessions](02-sessions-connexions.md) · [Espace](03-espace-bases.md) · [Réplication](04-replication.md) · [Sauvegardes](05-sauvegardes.md) · [Erreurs](06-erreurs-logs.md).

**Transmettre :** heure, impact, instance logique, erreur expurgée, test OK/KO, relevés et limites d'accès.

**Escalade immédiate :** indisponibilité métier, espace critique ou réplication attendue interrompue. Aucun redémarrage, `KILL`, `FLUSH` ou changement de configuration N1.

[Source : MySQL SHOW STATUS](https://dev.mysql.com/doc/refman/8.4/en/show-status.html)
