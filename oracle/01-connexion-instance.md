# ORA-N1-01 — Connexion, instance & rôle

**Quand ?** Timeout, ORA-01017, ORA-125xx, instance inconnue.

### Connexion (SQL*Plus)
```bash
sqlplus -L LECTURE@//HOST:1521/SERVICE
```
Saisir le mot de passe à l'invite, jamais dans le terminal ni sur GitHub.

### Identification (si droits sur V$)
```sql
SELECT instance_name, status, version_full, startup_time
FROM v$instance;

SELECT name, open_mode, database_role FROM v$database;
```

### Lecture rapide
- `ORA-01017` : authentification ou compte ; vérifier l'identifiant autorisé.
- `ORA-12514` / `ORA-12541` : service non connu du listener / listener non joignable ; vérifier la cible.
- `OPEN` = instance ouverte ; `READ WRITE` / `READ ONLY` = mode de la base.
- `PRIMARY` / `PHYSICAL STANDBY` = rôle Data Guard, **pas** rôle de l'instance RAC.
- Une instance peut être accessible tandis que la PDB métier ne l'est pas.

**Escalade :** heure, SERVICE_NAME, code ORA expurgé, impact, état attendu. Ne pas modifier listener, comptes ou services.

[Sources : V$INSTANCE](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-INSTANCE.html) · [Easy Connect](https://docs.oracle.com/en/database/oracle/oracle-database/26/netag/understanding-easy-connect-naming-method.html)
