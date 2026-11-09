# CASS-N1-04 — Stockage & tables

**Quand ?** Disque presque plein, forte croissance, SSTables nombreuses.

### État de stockage (JMX autorisé)
```bash
nodetool -h HOST tablestats KEYSPACE
nodetool -h HOST status
```

### Volumes OS (hôte autorisé)
```bash
df -h
df -i
```

### Lecture rapide
- `Space used (live)` et `Space used (total)` : données SSTable, pas capacité libre OS.
- `SSTable count` élevé peut être normal selon compaction et charge.
- `Load` du ring ≠ consommation de disque ; examiner **chaque nœud et volume**.
- Les snapshots et fichiers temporaires peuvent ajouter une consommation non visible dans la mesure de table.

**Escalade :** nœud, volume, saturation/tendance, keyspace, impact. Aucun nettoyage, `compact`, `cleanup` ou suppression de snapshot N1.

[Source : tablestats](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/tablestats.html)
