# REDIS-N1-01 — Connexion & identification

**Quand ?** `NOAUTH`, `WRONGPASS`, timeout ou mauvaise cible.

### Se connecter
```bash
redis-cli -h HOST -p PORT --tls --user LECTURE --askpass
```
Adapter CA/certificat et port à l'inventaire. Sans TLS, connexion uniquement si explicitement autorisée. Saisir le secret à l'invite.

### Dans redis-cli
```text
PING
INFO server
```

### Lecture rapide
- `redis_version` : version ; `redis_mode` : standalone, sentinel ou cluster.
- `NOAUTH` / `WRONGPASS` : authentification ou ACL ; ne pas exposer les identifiants.
- `Connection refused` / timeout : réseau, port, TLS, service ou endpoint.
- `PONG` ≠ santé applicative. `INFO` peut être interdit par les ACL.
- Les informations décrivent **le nœud interrogé**, pas nécessairement tout le service.

**Escalade :** heure, cible logique, erreur expurgée, version/mode, impact. Aucun changement ACL ou service N1.

[Sources : redis-cli](https://redis.io/docs/latest/develop/tools/cli/) · [INFO](https://redis.io/docs/latest/commands/info/)
