# CASS-N1-01 — Connexion & version

**Quand ?** CQL indisponible, `Unauthorized`, timeout, mauvaise cible.

### Connexion CQL (depuis un hôte autorisé)
```bash
cqlsh HOST 9042
# Utiliser le profil TLS/authentification validé de l'organisation.
```

### Dans cqlsh
```sql
SELECT cluster_name, release_version, data_center,
       rack, host_id FROM system.local;
```

### Lecture rapide
- `release_version` : version du nœud ciblé, pas nécessairement de tout le cluster.
- Timeout : réseau, endpoint CQL, TLS ou surcharge ; cause non confirmée.
- `Unauthorized` : autorisation ou authentification ; ne pas élever les droits N1.
- `9042` est le port CQL courant ; JMX/nodetool utilise un autre accès.

**Escalade :** heure, DC, nœud logique, erreur expurgée et impact. Aucun changement `cassandra.yaml` ou compte N1.

[Source : cqlsh](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/cqlsh.html)
