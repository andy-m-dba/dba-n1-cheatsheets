# MDB-N1-07 — Logs récents

**Quand ?** Erreurs récurrentes, problème de connexion, incident sans explication.

### Logs du processus (si commande autorisée)
```javascript
db.adminCommand({ getLog: "global" }).log.slice(-20)
```
Sur Atlas ou environnements supervisés, privilégier la console de logs autorisée.

### Sur Linux systemd (si accès hôte autorisé)
```bash
journalctl -u mongod --since "1 hour ago" --no-pager | tail -n 30
```
Le service peut porter un autre nom : vérifier l'inventaire.

### Lecture rapide
- `getLog` lit un **cache RAM limité aux 1024 événements récents**, pas tous les fichiers logs.
- Un message d'erreur proche de l'alerte n'établit pas automatiquement la cause.
- Les logs peuvent contenir des chemins, adresses, requêtes ou données sensibles : **expurger**.
- `Unauthorized` / sortie vide : comparer à la supervision et escalader si nécessaire.

**Escalade :** heure, code/message expurgé, fréquence, composant, impact. Ne pas supprimer de logs ni modifier la verbosité N1.

[Source : getLog](https://www.mongodb.com/docs/manual/reference/command/getlog/)
