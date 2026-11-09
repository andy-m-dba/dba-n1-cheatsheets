# CASS-N1-01 — Connexion & version

**Quand ?** CQL inaccessible, timeout ou erreur d'authentification.

### Connexion CQL
```bash
cqlsh HOST 9042
```
`9042` est le port courant, à vérifier dans l'inventaire. Utiliser `--ssl` lorsque TLS est requis et un profil `cqlshrc` / credentials protégé pour l'authentification. **Aucun mot de passe en argument.**

### Dans cqlsh
```sql
SELECT cluster_name, release_version, data_center,
       rack, host_id FROM system.local;
```

### Lecture rapide
- `release_version` : version **du nœud ciblé**, pas de tous les nœuds.
- Timeout : réseau, port CQL, TLS ou surcharge ; cause non établie.
- `Unauthorized` : droits CQL insuffisants ; erreur d'authentification : vérifier l'accès prévu.
- Une connexion CQL réussie ne prouve **pas** que le cluster entier est sain.

**Escalade :** heure, nœud/DC, erreur expurgée, accès OK/KO, impact. Aucun changement de compte ou `cassandra.yaml` N1.

[Source : cqlsh](https://cassandra.apache.org/doc/latest/cassandra/managing/tools/cqlsh.html)
