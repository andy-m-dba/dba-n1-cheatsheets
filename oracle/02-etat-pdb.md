# ORA-N1-02 — État des PDB

**Quand ?** Application indisponible alors que l'instance fonctionne.

### Vérifier le conteneur courant
```sql
SELECT SYS_CONTEXT('USERENV','CON_NAME') AS conteneur FROM dual;
```

### PDB visibles (avec droits adaptés)
```sql
SELECT name, open_mode, restricted
FROM v$pdbs
ORDER BY name;
```

### Lecture rapide
- `READ WRITE` : PDB ouverte en écriture.
- `READ ONLY` : peut être normal (notamment `PDB$SEED`).
- `MOUNTED` : PDB non ouverte aux connexions applicatives ordinaires.
- Depuis une PDB, la vue peut ne montrer **que cette PDB** ; depuis `CDB$ROOT`, vue plus étendue.
- Comparer l'état à l'inventaire et à la fenêtre de maintenance.

**Escalade :** PDB attendue fermée/restricted, erreur d'accès, impact. Aucun `ALTER PLUGGABLE DATABASE` en N1.

[Source : Monitoring des CDB/PDB](https://docs.oracle.com/en/database/oracle/oracle-database/19/multi/viewing-information-about-cdbs-and-pdbs-with-sql-plus.html)
