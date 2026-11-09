# MYSQL-N1-00 — Runbook express (5 min)

**Quand ?** Connexion KO, lenteurs, alerte MySQL ou MariaDB.

### 1. Relever (1 min)
Heure + fuseau, application, instance, erreur expurgée, impact.

### 2. Vérifier l'accès SQL (1 min)
```bash
mysql --host=HOST --port=3306 --user=LECTURE --password --execute="SELECT 1;"
# MariaDB : remplacer mysql par mariadb si nécessaire.
```
Le mot de passe est demandé à l'invite ; **ne pas l'écrire dans la commande**.

### 3. Si connexion possible (2 min)
```sql
SELECT @@version AS version, @@version_comment AS distribution,
       @@read_only AS lecture_seule;
SHOW GLOBAL STATUS WHERE Variable_name IN
 ('Threads_connected','Threads_running','Aborted_connects');
```

### 4. Orienter / escalader (1 min)
[Connexion](01-connexion-instance.md) · [Sessions](02-sessions-connexions.md) · [Espace](03-espace-bases.md) · [Réplication](04-replication.md) · [Backup](05-sauvegardes.md) · [Erreurs](06-erreurs-logs.md).

**Ticket :** heure, impact, instance, erreur expurgée, test SQL OK/KO, valeurs observées et contrôles impossibles.

**Escalade immédiate :** service indisponible, stockage critique, réplication attendue interrompue. Aucun redémarrage, `KILL`, `FLUSH` ou changement de configuration N1.

[Source : MySQL SHOW STATUS](https://dev.mysql.com/doc/refman/8.4/en/show-status.html)
