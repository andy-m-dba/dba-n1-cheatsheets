# REDIS-N1-06 — Erreurs & statistiques

**Quand ?** Erreurs récurrentes, refus d'accès ou incident intermittent.

### Dans redis-cli
```text
INFO stats
INFO errorstats
INFO server
```

### Lecture rapide
- `total_error_replies` et `errorstat_*` : compteurs d'erreurs **cumulatifs** ; relever deux mesures horodatées.
- `errorstats` peut être indisponible ou désactivé si le volume d'erreurs est excessif.
- `uptime_in_seconds` : repérer un redémarrage récent et contextualiser les compteurs.
- `NOAUTH` / `NOPERM` : accès ou ACL à qualifier ; une erreur ne prouve pas une panne du nœud.
- `INFO` peut être refusé par ACL ; ne collecter ni clés ni données métier.

**Escalade :** heure, compteurs avant/après, codes expurgés, impact. Aucun `CONFIG RESETSTAT`, `DEBUG` ou changement de configuration N1.

[Source : INFO](https://redis.io/docs/latest/commands/info/)
