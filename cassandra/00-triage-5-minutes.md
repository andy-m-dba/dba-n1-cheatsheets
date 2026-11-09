# CASS-N1-00 — Runbook express (5 min)

**Quand ?** Nœud indisponible, requêtes lentes, alerte Cassandra.

### 1. Identifier (1 min)
Heure + fuseau, cluster/DC, nœud, service touché, impact, alerte.

### 2. État du cluster (2 min, hôte et JMX autorisés)
```bash
nodetool -h HOST status
nodetool -h HOST info
```
`nodetool` utilise JMX (port habituel distinct de 9042). Adapter connexion et droits à l'inventaire.

### 3. Si CQL accessible (1 min)
```bash
cqlsh HOST 9042
```
Connexion via configuration TLS/authentification approuvée ; ne pas fournir de mot de passe sur la ligne de commande.

```sql
SELECT cluster_name, release_version, data_center FROM system.local;
```

### 4. Orienter / escalader (1 min)
[Connexion](01-connexion-version.md) · [Nœuds](02-etat-cluster.md) · [Charge](03-threads-activite.md) · [Stockage](04-stockage.md) · [Compactions](05-compactions-streaming.md) · [Backups](06-sauvegardes.md) · [Logs](07-logs.md).

**Escalade immédiate :** nœud `DN` inattendu, erreurs applicatives massives ou capacité critique. Transmettre état observé/attendu, heure, impact et limites de droits. Aucune réparation, bascule ou relance N1.

[Source : nodetool status](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/status.html)
