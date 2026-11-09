# CASS-N1-03 — Files d'attente & activité

**Quand ?** Latence, timeouts, surcharge de thread pools.

### Commandes (JMX autorisé)
```bash
nodetool -h HOST tpstats
nodetool -h HOST info
```

### Lecture rapide
- `Pending` : tâches en attente ; comparer à la tendance et au comportement habituel.
- `Blocked` : tâches en blocage dans un pool, à contextualiser.
- `Dropped` : messages abandonnés, compteurs souvent cumulés ; comparer deux relevés.
- `info` : uptime, heap et état du nœud ; la heap n'est pas toute la mémoire OS.
- Une mesure ponctuelle ne permet pas de conclure à une saturation durable.

**Escalade :** nœud, pool, Pending/Dropped, heure, erreurs et impact. Ne pas modifier les pools, la JVM ou les timeouts en N1.

[Source : nodetool](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/nodetool.html)
