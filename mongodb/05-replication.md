# MDB-N1-05 — Réplication (Replica Set)

**Quand ?** Secondaire absent, élection, réplication en retard.

### Rôle du nœud ciblé
```javascript
const h = db.adminCommand({ hello: 1 })
({ set: h.setName, primary: h.isWritablePrimary,
   secondary: h.secondary, mongos: h.msg === "isdbgrid" })
```

### Membres du replica set (avec droits de supervision)
```javascript
rs.status().members.map(m => ({
  name: m.name, state: m.stateStr,
  health: m.health, optimeDate: m.optimeDate
}))
```

### Lecture rapide
- `PRIMARY` = primaire ; `SECONDARY` = réplique.
- `RECOVERING` / `DOWN` : comparer à la topologie attendue.
- `optimeDate` est un indicateur ponctuel, **pas une mesure de lag complète**.
- `rs.status()` nécessite `replSetGetStatus` et une connexion à **mongod** membre d'un replica set (pas `mongos`).
- Sur Atlas Free/Flex, la commande peut être indisponible : utiliser les métriques Atlas.

**Escalade :** membre, état attendu/observé, heure, alerte. Aucun `rs.stepDown()`, `rs.reconfig()` ou `rs.syncFrom()` N1.

[Source : replSetGetStatus](https://www.mongodb.com/docs/manual/reference/command/replsetgetstatus/)
