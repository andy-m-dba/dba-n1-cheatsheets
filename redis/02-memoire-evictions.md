# REDIS-N1-02 — Mémoire & évictions

**Quand ?** Alerte `maxmemory`, OOM, évictions ou hausse mémoire.

### Dans redis-cli (lecture)
```text
INFO memory
INFO stats
```

### Lecture rapide
- `used_memory` : mémoire allouée par Redis ; `used_memory_rss` : mémoire résidente du processus.
- `maxmemory = 0` : pas de plafond Redis défini ; la limite système reste possible.
- `evicted_keys` : compteur cumulé d'évictions ; comparer deux relevés horodatés.
- `mem_fragmentation_ratio` isolé ne prouve pas une fuite mémoire.
- En cluster : contrôler les métriques **de chaque nœud**, pas un seul.

**Escalade :** mémoire, plafond, évolution des évictions, impact. Ne pas purger de clés, déclencher `MEMORY PURGE` ou changer `maxmemory` N1.

[Source : INFO](https://redis.io/docs/latest/commands/info/)
