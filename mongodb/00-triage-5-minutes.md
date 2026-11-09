# MDB-N1-00 — Runbook express (5 min)

**Quand ?** Connexion KO, application lente, alerte MongoDB.

### 1. Identifier (1 min)
Heure + fuseau, cluster/service, application touchée, erreur **expurgée**, impact.

### 2. Se connecter (1 min)
```bash
mongosh "mongodb://HOST:27017/admin" --username LECTURE --authenticationDatabase admin
# Mot de passe demandé à l'invite ; adapter port, TLS et authSource à l'inventaire.
```

### 3. Vérifier (2 min, dans mongosh)
```javascript
db.adminCommand({ ping: 1 })
const h = db.adminCommand({ hello: 1 })
({ primary: h.isWritablePrimary, secondary: h.secondary,
   replicaSet: h.setName, mongos: h.msg === "isdbgrid" })
```
`ping: ok: 1` vérifie la réponse du serveur ciblé, **pas** la santé applicative.

### 4. Orienter / escalader (1 min)
[Connexion](01-connexion-version.md) · [Bases](02-bases-collections.md) · [Opérations](03-operations-connexions.md) · [Espace](04-espace-stockage.md) · [Réplication](05-replication.md) · [Backup](06-sauvegardes.md) · [Logs](07-logs.md).

**Ticket :** heure, impact, cible logique, message expurgé, `ping` OK/KO, rôle, état attendu et relevé ; noter toute limitation de droits.

**Escalade immédiate** si service indisponible, perte potentielle de données, primaire attendu absent ou stockage critique. Aucun redémarrage, `stepDown`, `killOp` ou suppression N1.

[Source : connexion mongosh](https://www.mongodb.com/docs/mongodb-shell/connect/)
