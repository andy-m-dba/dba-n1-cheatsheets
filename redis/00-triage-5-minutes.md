# REDIS-N1-00 — Runbook express (5 min)

**Quand ?** Redis inaccessible, réponses lentes, alerte mémoire ou réplication.

### 1. Relever (1 min)
Heure + fuseau, service/cluster, impact, alerte et erreur expurgée.

### 2. Connexion (1 min)
```bash
redis-cli -h HOST -p PORT --tls --user LECTURE --askpass
# Adapter le certificat CA/TLS à la politique locale.
```
**Ne jamais placer le secret dans la ligne de commande.** Sans TLS, utiliser uniquement une connexion explicitement autorisée.

### 3. Dans redis-cli (2 min)
```text
PING
INFO server
INFO clients
INFO memory
```
`PONG` = réponse de ce nœud ; **pas** une preuve de santé applicative ou cluster.

### 4. Orienter / escalader (1 min)
[Connexion](01-connexion-version.md) · [Mémoire](02-memoire-evictions.md) · [Clients](03-clients-latence.md) · [Réplication](04-replication-cluster.md) · [Persistance](05-persistance-backups.md) · [Erreurs](06-erreurs-stats.md).

**Ticket :** heure, impact, cible, `PING`, valeurs relevées, anomalies et commandes refusées par les ACL.

**Escalade immédiate :** indisponibilité, OOM, `cluster_state:fail`, réplica critique absent. Aucun `FLUSHALL`, `CONFIG SET`, `FAILOVER` ou redémarrage N1.

[Source : redis-cli](https://redis.io/docs/latest/develop/tools/cli/)
