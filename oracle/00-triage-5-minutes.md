# ORA-N1-00 — Runbook express (5 min)

**Quand ?** ORA-xxxxx, connexion impossible, base lente ou alerte.

### 1. Identifier (1 min)
Heure + fuseau, service/PDB visé, alerte exacte, impact métier.

### 2. Tester la connexion (1 min)
```bash
sqlplus -L LECTURE@//HOST:1521/SERVICE
# Mot de passe saisi à l'invite, jamais sur la ligne de commande
```
`1521` est un exemple : utiliser le port et le SERVICE_NAME réels.

### 3. Vérifier l'état (2 min, si droits autorisés)
```sql
SELECT instance_name, status, database_status FROM v$instance;
SELECT name, open_mode, database_role FROM v$database;
```
Une vue inaccessible (`ORA-00942` ou droits insuffisants) **ne prouve pas** une panne.

### 4. Orienter / escalader (1 min)
[Connexion](01-connexion-instance.md) · [PDB](02-etat-pdb.md) · [Sessions](03-sessions-blocages.md) · [Espace](04-tablespaces-fra.md) · [RMAN](05-sauvegardes.md) · [Data Guard](06-data-guard.md) · [Alert log](07-alert-log.md).

**Ticket :** heure, impact, service ciblé, code ORA expurgé, connexion OK/KO, état observé/attendu, contrôles impossibles.

**Escalade immédiate :** indisponibilité métier, erreur critique, risque de perte de données ou saturation. Aucun `STARTUP`, `SHUTDOWN`, `ALTER SYSTEM` ou basculement N1.

[Source : V$INSTANCE](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-INSTANCE.html)
