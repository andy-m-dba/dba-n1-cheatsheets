# CASS-N1-05 — Compactions & streaming

**Quand ?** Charge disque, lenteur, changement de topologie en cours.

### Commandes (JMX autorisé)
```bash
nodetool -h HOST compactionstats
nodetool -h HOST netstats
```

### Lecture rapide
- `compactionstats` : compactions actives/en attente ; vérifier la durée et la tendance.
- `netstats` : streaming et activité réseau ; peut être normal lors d'un bootstrap ou rebuild planifié.
- La présence d'une compaction ne prouve pas un incident ; comparer au comportement attendu.
- Une activité absente peut aussi être normale ; les vues sont **ponctuelles**.

**Escalade :** nœud, tâches, progression, opérations planifiées et impact. Ne lancer ni `repair`, `compact`, `rebuild` ni `cleanup` N1.

[Sources : compactionstats](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/compactionstats.html) · [netstats](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/netstats.html)
