# REDIS-N1-01 — Connexion & version

**Quand ?** `NOAUTH`, `WRONGPASS`, `ECONNREFUSED`, cible incertaine.

### Connexion (TLS selon inventaire)
```bash
redis-cli -h HOST -p PORT --tls --user LECTURE --askpass
```
Adapter les paramètres CA/certificat à l'environnement.

### Dans redis-cli
```text
PING
INFO server
```

### Lecture rapide
- `redis_version` : version ; `redis_mode` : standalone, sentinel ou cluster.
- `NOAUTH` / `WRONGPASS` : erreur de connexion/ACL ; ne jamais exposer le secret.
- Timeout : DNS, réseau, TLS, service ou endpoint ; cause à confirmer.
- `PONG` ne prouve pas que toutes les opérations de l'application réussissent.
- `INFO` peut être interdit par les ACL : utiliser les métriques de supervision.

**Escalade :** heure, endpoint logique, erreur expurgée, mode, version et impact. Aucune modification ACL N1.

[Sources : redis-cli](https://redis.io/docs/latest/develop/tools/cli/) · [INFO](https://redis.io/docs/latest/commands/info/)
