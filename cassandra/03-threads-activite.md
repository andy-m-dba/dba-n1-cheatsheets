# CASS-N1-03 — Activité & files d'attente

**Quand ?** Timeouts, hausse de latence ou surcharge du nœud.

### Commandes (JMX autorisé)
```bash
nodetool -h HOST tpstats
nodetool -h HOST info
```

### Lecture rapide
- `Active` : tâches en cours dans un pool ; `Pending` : tâches en attente.
- `Blocked` : tâches bloquées dans le pool ; comparer à la situation normale.
- `Dropped` : messages abandonnés ; **compteur cumulatif** à comparer sur deux relevés horodatés.
- `info` : uptime, load et heap ; la heap JVM ne représente pas toute la RAM du serveur.
- Une file momentanée n'est pas une preuve de saturation durable.

**Escalade :** nœud, pool concerné, Pending/Dropped, tendance, heure et impact. Aucun réglage des pools ou de la JVM N1.

[Source : dépannage via nodetool](https://cassandra.apache.org/doc/stable/cassandra/troubleshooting/use_nodetool.html)
