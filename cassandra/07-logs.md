# CASS-N1-07 — Logs & erreurs

**Quand ?** Timeout CQL, erreur répétée ou nœud instable.

### Journal systemd (si utilisé et accès autorisé)
```bash
journalctl -u cassandra --since "1 hour ago" --no-pager | tail -n 30
```
Sinon, consulter `system.log` / les journaux configurés via le chemin **approuvé dans l'inventaire** ou la supervision.

### Lecture rapide
- Rechercher `ERROR`, exceptions, timeouts, anomalies de disque ou de JVM.
- Une erreur dans les logs ne prouve pas à elle seule la cause de l'incident.
- Absence d'événement dans `journalctl` ≠ absence de logs Cassandra.
- Expurger chemins, adresses, identifiants et requêtes ; vérifier heure et fuseau.

**Escalade :** nœud, heure, message expurgé, répétition et impact. Ne pas supprimer de logs ni changer leur niveau N1.

[Source : dépannage Cassandra](https://cassandra.apache.org/doc/stable/cassandra/troubleshooting/use_nodetool.html)
