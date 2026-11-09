# MSSQL-N1-00 — Runbook express (5 min)

**Quand ?** SQL Server inaccessible, application lente, alerte base.

### 1. Relever (1 min)
Heure + fuseau, application, impact, message d'erreur **expurgé**, instance attendue.

### 2. Tester le réseau (1 min, PowerShell Windows)
```powershell
Test-NetConnection -ComputerName SERVEUR -Port 1433
```
Utiliser le **port TCP réel** de l'instance (1433 n'est qu'une valeur fréquente). Un port joignable ne valide ni l'authentification ni la base.

### 3. Si connexion SQL autorisée (2 min)
```sql
SELECT @@SERVERNAME AS instance, @@VERSION AS version_sql;
SELECT name, state_desc FROM sys.databases ORDER BY name;
```

Voir [connexion](01-connexion-instance.md) · [bases](02-etat-bases.md) · [sessions](03-sessions-blocages.md) · [disque](04-espace-fichiers.md) · [backups](05-sauvegardes.md) · [Always On](06-always-on.md).

### 4. Transmettre (1 min)
```text
Heure / impact :
Instance / base ciblée :
Erreur expurgée :
Test TCP : OK / KO / non testé
Connexion SQL : OK / KO
Bases hors ONLINE (si visibles) :
Vérifications impossibles / droits insuffisants :
```

**Escalade immédiate** si indisponibilité métier, base `SUSPECT`/`RECOVERY_PENDING`, perte potentielle de données ou saturation. Ne pas redémarrer, changer la configuration ni lancer de failover.

[Source : sys.databases](https://learn.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)
