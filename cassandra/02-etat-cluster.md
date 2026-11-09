# CASS-N1-02 — État du cluster

**Quand ?** Nœud `DN`, état de topologie inhabituel, incident multi-DC.

### Commandes (JMX autorisé)
```bash
nodetool -h HOST status
nodetool -h HOST describecluster
```

### Lecture rapide
- **1re lettre** : `U` = Up, `D` = Down ; **2e lettre** : `N` = Normal, `J` = Joining, `L` = Leaving, `M` = Moving.
- `UN` : nœud Up / Normal. `DN` inattendu : incident à qualifier immédiatement.
- `Load` : volume de données local, **pas** pourcentage de disque occupé.
- `describecluster` : nom du cluster, partitioner et versions de schéma observées.
- `status` affiche la **vue du nœud interrogé** : des nœuds peuvent avoir des perceptions différentes.

**Escalade :** DC, nœuds concernés, état attendu/observé, heure, impact. Aucun `decommission`, `removenode` ou `repair` N1.

[Sources : status](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/status.html) · [describecluster](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/describecluster.html)
