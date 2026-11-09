# MDB-N1-04 — Espace & stockage

**Quand ?** Disque presque plein, croissance des données, alerte WiredTiger.

### Taille de la base ciblée (avec droits adaptés)
```javascript
db.getSiblingDB("DATABASE").runCommand({ dbStats: 1, scale: 1024 * 1024 })
```
Résultats en MiB (pour les champs de taille scalés).

### Disque Linux (si accès hôte autorisé)
```bash
df -h
df -i
```
Sur Atlas : consulter les métriques **Disk / Storage** de la console.

### Lecture rapide
- `dataSize` : taille logique (non compressée) des documents.
- `storageSize` : espace alloué aux collections ; `indexSize` : index.
- La somme SQL logique ne correspond **pas** à l'espace libre de l'OS.
- En cluster sharded, vérifier les métriques par shard et la supervision.

**Escalade :** volume/shard, taux et tendance, base, impact. Ne pas lancer `compact`, supprimer de fichiers ni changer les quotas N1.

[Source : dbStats](https://www.mongodb.com/docs/manual/reference/command/dbstats/)
