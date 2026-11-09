# CASS-N1-06 — Sauvegardes

**Quand ?** Snapshot attendu absent, job en échec, alerte RPO.

### Vérifier l'état des backups incrémentaux (JMX autorisé)
```bash
nodetool -h HOST statusbackup
```

### Vérifier dans l'outil officiel
Ordonnanceur, snapshots, sauvegarde managée, stockage distant : relever dernier succès, type, couverture des nœuds/DC et rétention.

### Lecture rapide
- `statusbackup` renseigne l'**activation des sauvegardes incrémentales**, pas le succès d'un job ou la présence d'un snapshot.
- Un snapshot local sur un nœud ne prouve pas la protection complète du cluster.
- Une sauvegarde indiquée `success` ne garantit pas qu'une restauration ait été testée.
- Comparer à la fréquence et au RPO/RTO internes.

**Escalade :** job, couverture, dernier succès, RPO, erreur expurgée. Aucun `snapshot`, `clearsnapshot` ni restauration N1.

[Source : statusbackup](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/statusbackup.html)
