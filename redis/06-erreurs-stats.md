# REDIS-N1-06 — Erreurs & statistiques

**Quand ?** Hausse des erreurs, refus de connexion, incident intermittent.

### Dans redis-cli
```text
INFO stats
INFO errorstats
INFO server
```

### Lecture rapide
- `total_error_replies` et `errorstat_*` (si exposés) : **compteurs cumulés**, comparer deux relevés.
- `uptime_in_seconds` : identifier un redémarrage récent.
- Certains champs/sections varient selon la version et l'offre.
- Les erreurs `NOAUTH` / ACL peuvent provenir d'un mauvais client, sans confirmer une panne du serveur.
- Ne collecter ni valeurs de clés ni données métier dans un ticket.

**Escalade :** heure, compteur précédent/nouveau, erreur expurgée, impact. Aucun `CONFIG SET`, `DEBUG` ni reset des statistiques N1.

[Source : INFO](https://redis.io/docs/latest/commands/info/)
