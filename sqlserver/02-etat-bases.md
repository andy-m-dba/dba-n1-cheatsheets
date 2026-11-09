# MSSQL-N1-02 — État des bases

**Quand ?** Base inaccessible, alerte `OFFLINE`, `SUSPECT` ou `RECOVERY_PENDING`.

### Commande
```sql
SELECT name, state_desc, user_access_desc,
       recovery_model_desc
FROM sys.databases
ORDER BY name;
```

### Lecture rapide
| État | Signification N1 |
|---|---|
| `ONLINE` | Base en ligne ; pas une preuve de santé applicative |
| `RESTORING` | Restauration en cours ou état attendu pour certains secondaires |
| `RECOVERING` | Récupération en cours ; comparer à l'état attendu |
| `RECOVERY_PENDING` | Récupération impossible à démarrer : escalade |
| `SUSPECT` | État critique : escalade immédiate |
| `OFFLINE` | Vérifier maintenance planifiée / attente |

Une base absente peut être **masquée par les droits**. Vérifier la visibilité autorisée avant de conclure.

**Escalade :** nom logique de base, état observé/attendu, heure et impact. Ne pas lancer `ALTER DATABASE`, `DBCC CHECKDB` ni `RESTORE` de sa propre initiative N1.

[Source : sys.databases](https://learn.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)
