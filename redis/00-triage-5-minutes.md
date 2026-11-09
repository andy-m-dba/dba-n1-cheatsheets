# REDIS-N1-00 — Runbook express (5 min)

**Quand ?** Redis inaccessible, lenteur, alerte mémoire ou réplication.

### 1. Identifier (1 min)
Heure et fuseau, service/nœud, application, erreur expurgée, impact.

### 2. Se connecter (1 min)
```bash
redis-cli -h HOST -p PORT --tls --user LECTURE --askpass
```
Adapter TLS (CA/certificat), port et ACL à l'inventaire. Désactiver `--tls` **uniquement** si la connexion non chiffrée est autorisée. Mot de passe à l'invite, jamais en argument.

### 3. Vérifier (2 min, dans redis-cli)
```text
PING
INFO server
INFO clients
INFO memory
```
`PONG` confirme la réponse du nœud, **pas** la santé de l'application ni du cluster. `INFO` peut être interdit par ACL.

### 4. Orienter et escalader (1 min)
[Connexion](01-connexion-version.md) · [Mémoire](02-memoire-evictions.md) · [Clients](03-clients-latence.md) · [Réplication](04-replication-cluster.md) · [Persistance](05-persistance-backups.md) · [Erreurs](06-erreurs-stats.md).

**Transmettre :** heure, impact, cible logique, `PING` OK/KO, compteurs et accès refusés.

**Escalade immédiate :** indisponibilité, OOM, `cluster_state:fail` ou réplica attendu absent. Aucun redémarrage, `FLUSHALL`, `CONFIG SET` ou failover N1.

[Source : redis-cli](https://redis.io/docs/latest/develop/tools/cli/)
