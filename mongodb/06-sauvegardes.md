# MDB-N1-06 — Sauvegardes

**Quand ?** Snapshot absent, job échoué, alerte RPO.

### Vérifier dans l'outil de sauvegarde (lecture seule)
- **Atlas** : projet → cluster → Backup → Snapshots (selon l'offre).
- **Self-managed** : Ops Manager / Cloud Manager / ordonnanceur / snapshots validés.
- **mongodump** : vérifier le job externe ; `mongosh` ne donne pas un statut universel de réussite.

### Lecture rapide
- Dernière sauvegarde réussie : comparer à la fréquence et au **RPO** attendus.
- Un snapshot `Completed` ne prouve pas la restaurabilité : seul un test de restauration autorisé la confirme.
- `Point-in-Time Recovery` dépend de la solution et de sa configuration.
- Absence de backup visible peut venir des droits ou de l'offre : ne pas conclure sans vérification.

**Escalade :** cluster, type, dernière réussite, statut, RPO, erreur expurgée. Ne jamais lancer de restauration ou de purge N1.

[Source : Atlas Backup](https://www.mongodb.com/docs/atlas/backup/cloud-backup/overview/)
