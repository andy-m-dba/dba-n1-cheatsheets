# CASS-N1-05 — Compactions & streaming

**Quand ?** Lenteur disque, tâches en attente ou mouvement de données inattendu.

### Commandes (JMX autorisé)
```bash
nodetool -h HOST compactionstats
nodetool -h HOST netstats
```

### Lecture rapide
- `compactionstats` : compactions actives, tâches en attente et progression estimée.
- `netstats` : sessions de streaming et informations réseau visibles depuis ce nœud.
- Une compaction ou un streaming peuvent être normaux pendant une maintenance planifiée.
- Une durée estimée n'est **pas** une garantie de fin ; comparer deux relevés et l'impact.
- Aucune activité visible n'exclut pas un autre problème de performance.

**Escalade :** nœud, opérations visibles, progression, heure et impact. Aucun `repair`, `compact`, `rebuild` ou `cleanup` N1.

[Sources : compactionstats](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/compactionstats.html) · [netstats](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/netstats.html)
