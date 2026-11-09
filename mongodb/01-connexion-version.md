# MDB-N1-01 — Connexion & version

**Quand ?** Timeout, échec d'authentification, hôte/port ou rôle incertain.

### Connexion
```bash
mongosh "mongodb://HOST:27017/admin" --username LECTURE --authenticationDatabase admin
```
Mot de passe saisi à l'invite. **Ne pas mettre de secret dans l'URI ou l'historique.** Adapter TLS, SRV et authentification à la configuration autorisée.

### Dans mongosh
```javascript
db.adminCommand({ ping: 1 })
db.adminCommand({ buildInfo: 1 }).version
const h = db.adminCommand({ hello: 1 })
({ primary: h.isWritablePrimary, secondary: h.secondary,
   replicaSet: h.setName, mongos: h.msg === "isdbgrid" })
```

### Lecture rapide
- `Authentication failed` : identifiant, base d'authentification ou politique d'accès.
- `ECONNREFUSED` / `ETIMEDOUT` : cible, réseau, service ou filtrage.
- `mongos: true` : routeur de cluster sharded ; ne pas y appliquer `rs.status()`.
- `primary: true` : nœud acceptant les écritures **à cet instant**, pas une validation complète du cluster.

**Escalade :** heure, version, rôle, erreur expurgée, impact. Aucun changement de compte ou config.

[Sources : mongosh](https://www.mongodb.com/docs/mongodb-shell/connect/) · [buildInfo](https://www.mongodb.com/docs/manual/reference/command/buildinfo/)
