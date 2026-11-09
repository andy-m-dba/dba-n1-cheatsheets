# MYSQL-N1-06 — Erreurs & logs

**Quand ?** Connexions rejetées, alerte répétée, incident sans diagnostic.

### Indicateurs SQL
```sql
SHOW GLOBAL STATUS LIKE 'Aborted_connects';
SHOW GLOBAL STATUS LIKE 'Uptime';
SHOW GLOBAL VARIABLES LIKE 'log_error';
```

### Logs (sur hôte autorisé)
Utiliser le chemin du journal indiqué par **l'inventaire** ou `log_error`, puis l'outil de supervision ; ne pas supposer qu'il existe toujours un fichier.

### Lecture rapide
- `Aborted_connects` est cumulatif depuis un reset/démarrage : comparer **deux relevés horodatés**.
- `log_error` localise la configuration, pas forcément la destination effective dans un service managé.
- Un message proche dans le temps n'établit pas à lui seul la cause.
- Expurger les IP, chemins, comptes et requêtes avant partage.

**Escalade :** heure, code erreur, fréquence, impact. Ne modifier ni niveau de logs ni fichiers N1.

[Source : MySQL Server Status](https://dev.mysql.com/doc/refman/8.4/en/server-status-variables.html)
