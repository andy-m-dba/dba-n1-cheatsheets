# MDB-N1-03 — Opérations & connexions

**Quand ?** Lenteurs, opérations longues, trop de connexions.

### Connexions au processus (avec rôle de supervision)
```javascript
db.serverStatus().connections
```

### Opérations longues (avec privilège `inprog`)
```javascript
db.getSiblingDB("admin").aggregate([
  { $currentOp: { allUsers: true, idleConnections: false } },
  { $match: { active: true, secs_running: { $gte: 5 } } },
  { $project: { _id: 0, opid: 1, secs_running: 1,
                op: 1, ns: 1, waitingForLock: 1 } },
  { $limit: 10 }
])
```

### Lecture rapide
- `current` = connexions ouvertes ; comparer au niveau habituel, pas à un seuil universel.
- `5` secondes n'est **qu'un filtre d'exemple**, pas un seuil d'incident.
- Une opération longue n'est pas nécessairement bloquée ; une sortie vide est ponctuelle.
- `Unauthorized` : relever le manque de droits. Sur Atlas Free/Flex, certaines commandes sont indisponibles.
- Ne pas afficher ni partager les commandes métier potentiellement sensibles.

**Escalade :** heure, connexions, durée/opid, impact. Ne jamais lancer `killOp` ni activer le profiler N1.

[Sources : serverStatus](https://www.mongodb.com/docs/manual/reference/method/db.serverstatus/) · [$currentOp](https://www.mongodb.com/docs/manual/reference/operator/aggregation/currentOp/)
