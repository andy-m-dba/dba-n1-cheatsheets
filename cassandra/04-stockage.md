# CASS-N1-04 — Stockage & tables

**Quand ?** Volume presque plein, hausse des SSTables ou croissance anormale.

### Statistiques d'une keyspace (JMX autorisé)
```bash
nodetool -h HOST tablestats KEYSPACE
```

### Volumes OS (sur l'hôte autorisé)
```bash
df -h
df -i
```

### Lecture rapide
- `Space used (live)` / `Space used (total)` : volumes des SSTables, **pas** espace libre du filesystem.
- `SSTable count` : nombre de SSTables ; dépend de la charge et de la stratégie de compaction.
- Snapshots, commitlogs et temporaires peuvent occuper de l'espace hors du total de table.
- Vérifier les volumes et **chaque nœud**, pas seulement la keyspace interrogée.

**Escalade :** nœud, volume, occupation/tendance, keyspace et impact. Aucun `compact`, `cleanup` ni suppression de snapshots N1.

[Source : tablestats](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/tablestats.html)
