# CASS-N1-07 — Logs récents

**Quand ?** Erreurs CQL, timeout, nœud instable, alerte inexpliquée.

### Sur Linux (hôte autorisé)
```bash
journalctl -u cassandra --since "1 hour ago" --no-pager | tail -n 30
```
Si Cassandra n'utilise pas systemd, lire le journal de l'instance via la supervision autorisée.

### Lecture rapide
- Repérer `ERROR`, timeouts, exceptions et messages de disque/JVM.
- Les logs peuvent contenir adresses, chemins, requêtes ou données sensibles : expurger.
- Absence de message récent dans journald ne prouve pas que Cassandra n'a rien journalisé.
- Corréler heure/fuseau et indicateurs `nodetool` avant de conclure.

**Escalade :** nœud, heure, message expurgé, fréquence, impact. Ne supprimer ni logs ni données, ne modifier aucun niveau de log N1.

[Source : dépannage Cassandra](https://cassandra.apache.org/doc/stable/cassandra/troubleshooting/use_nodetool.html)
