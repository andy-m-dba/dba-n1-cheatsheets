# MDB-N1-02 — Bases & collections

**Quand ?** Base/collection non visible, erreur `NamespaceNotFound`, accès applicatif KO.

### Bases accessibles au compte
```javascript
db.adminCommand({ listDatabases: 1, nameOnly: true, authorizedDatabases: true })
```

### Collections visibles dans une base
```javascript
db.getSiblingDB("DATABASE").getCollectionNames()
```

### Lecture rapide
- Liste vide ou base absente **≠ suppression** : l'accès dépend des privilèges.
- Une collection inexistante peut correspondre à une mauvaise base, casse ou cible.
- Une base existe dans l'inventaire mais reste inaccessible ? Noter erreur et contexte.
- Ne pas exécuter de `find()` sans filtre sur les collections métier : données sensibles et charge.

**Escalade :** base/collection attendue, réponse observée, erreur, compte de lecture et impact. Aucune création, suppression ou changement de rôles N1.

[Source : listDatabases](https://www.mongodb.com/docs/manual/reference/command/listdatabases/)
