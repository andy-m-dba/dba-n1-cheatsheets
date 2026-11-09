# MSSQL-N1-01 — Connexion & instance

**Quand ?** Timeout, login refusé, instance ou version inconnue.

### Test (SSMS ou sqlcmd déjà configuré)
```sql
SELECT @@SERVERNAME AS instance,
       SERVERPROPERTY('ProductVersion') AS version,
       SERVERPROPERTY('Edition') AS edition,
       DB_NAME() AS base_courante,
       SYSTEM_USER AS login_courant;
```

Test réseau Windows, **port réel** relevé dans l'inventaire :
```powershell
Test-NetConnection -ComputerName SERVEUR -Port 1433
```

### Lecture rapide
- `Login failed` : identité/authentification/permissions à vérifier.
- `Timeout` : résolution DNS, réseau, écoute ou charge ; cause non établie.
- TCP OK ≠ connexion SQL réussie. Vérifier le serveur et l'instance attendus.
- Une instance nommée peut écouter sur un port différent de 1433.

**Escalade :** heure, cible logique, erreur expurgée, résultat TCP et impact. Ne changer ni compte, ni service, ni protocole.

[Source : SERVERPROPERTY](https://learn.microsoft.com/en-us/sql/t-sql/functions/serverproperty-transact-sql)
