# REDIS-N1-02 — Mémoire & évictions

**Quand ?** OOM, limite `maxmemory`, hausse mémoire ou clés évincées.

### Dans redis-cli
```text
INFO memory
INFO stats
```

### Lecture rapide
- `used_memory` : mémoire allouée par Redis ; `used_memory_rss` : mémoire résidente vue par l'OS.
- `maxmemory = 0` : pas de plafond Redis configuré ; la limite système reste applicable.
- `evicted_keys` : évictions liées à la politique `maxmemory` ; **compteur cumulatif** à comparer entre deux relevés.
- `mem_fragmentation_ratio` isolé ne prouve pas une fuite mémoire.
- En cluster, chaque nœud a ses propres métriques ; ne pas conclure sur un seul nœud.

**Escalade :** heure, `used_memory`, `maxmemory`, évolution de `evicted_keys`, impact. Aucune purge de clés, `MEMORY PURGE` ou modification `maxmemory` N1.

[Sources : INFO](https://redis.io/docs/latest/commands/info/) · [Évictions](https://redis.io/docs/latest/reference/eviction/)
