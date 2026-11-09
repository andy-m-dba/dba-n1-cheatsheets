# CASS-N1-06 — Sauvegardes & snapshots

**Quand ?** Snapshot absent, backup en échec ou alerte RPO.

### Contrôles locaux (JMX autorisé)
```bash
nodetool -h HOST statusbackup
nodetool -h HOST listsnapshots
```

### Lecture rapide
- `statusbackup` : **activation** des backups incrémentaux, pas leur réussite.
- `listsnapshots` : snapshots présents sur **ce nœud** ; un snapshot local ne couvre pas forcément tout le cluster.
- Snapshot présent ≠ sauvegarde transférée, complète ou restaurable.
- Vérifier dans l'outil officiel : dernier succès, couverture des nœuds/DC, rétention et RPO.
- Un résultat `success` ne remplace pas un test de restauration autorisé.

**Escalade :** job, dernière réussite, nœuds couverts, RPO, erreur expurgée. Aucun `snapshot`, `clearsnapshot` ni restauration N1.

[Sources : statusbackup](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/statusbackup.html) · [listsnapshots](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/nodetool/listsnapshots.html)
