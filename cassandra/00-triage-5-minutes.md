# CASS-N1-00 — Runbook express (5 min)

**Quand ?** Nœud indisponible, timeouts CQL ou alerte Cassandra.

### 1. Identifier (1 min)
Heure et fuseau, cluster/DC, nœud ciblé, application, erreur expurgée, impact.

### 2. Vérifier le cluster (2 min, accès JMX autorisé)
```bash
nodetool -h HOST status
nodetool -h HOST info
```
`nodetool` utilise JMX, **pas** le port CQL 9042. Adapter hôte, port JMX et authentification à l'inventaire.

### 3. Si CQL est accessible (1 min)
```bash
cqlsh HOST 9042
```
Utiliser le profil TLS et les identifiants autorisés, sans mot de passe sur la ligne de commande.

```sql
SELECT cluster_name, release_version, data_center FROM system.local;
```

### 4. Orienter et escalader (1 min)
[Connexion](01-connexion-version.md) · [Cluster](02-etat-cluster.md) · [Activité](03-threads-activite.md) · [Stockage](04-stockage.md) · [Compactions](05-compactions-streaming.md) · [Sauvegardes](06-sauvegardes.md) · [Logs](07-logs.md).

**Transmettre :** heure, impact, état attendu/observé, codes d'erreur et diagnostics impossibles (droits/JMX).

**Escalade immédiate :** nœud `DN` inattendu, panne métier ou stockage critique. Aucun redémarrage, `repair` ni changement de topologie N1.

[Source : nodetool status](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/status.html)
