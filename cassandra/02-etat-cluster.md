# CASS-N1-02 — État du cluster

**Quand ?** Nœud `DN`, état Joining/Leaving, incident multi-DC.

### Sur un point JMX autorisé
```bash
nodetool -h HOST status
nodetool -h HOST describecluster
```

### Lecture rapide
- `UN` = Up / Normal ; `DN` = Down / Normal.
- `UJ` / `UL` / `UM` : nœud up en changement de topologie ; comparer aux opérations planifiées.
- `Load` = charge de données sur nœud, **pas** pourcentage de disque utilisé.
- Le statut est vu **depuis le nœud interrogé** ; comparer depuis d'autres nœuds autorisés si résultats incohérents.
- `describecluster` aide à constater une divergence de schéma ; ne pas modifier.

**Escalade :** cluster/DC, nœuds attendus/observés, statut, heure, impact. Aucun `decommission`, `removenode`, `assassinate` ou `repair` N1.

[Source : nodetool status](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/status.html)
