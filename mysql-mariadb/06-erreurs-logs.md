# MYSQL-N1-06 — Erreurs & logs

**Quand ?** Connexions rejetées, erreur récurrente ou alerte sans cause claire.

### Compteurs et configuration
```sql
SHOW GLOBAL STATUS LIKE 'Aborted_connects';
SHOW GLOBAL STATUS LIKE 'Uptime';
SHOW GLOBAL VARIABLES LIKE 'log_error';
```

### Consulter les logs
Utiliser l'outil de supervision ou le chemin **autorisé** de l'inventaire. Sur une offre managée, les logs peuvent être accessibles uniquement depuis sa console.

### Lecture rapide
- `Aborted_connects` : compteur cumulatif ; comparer deux relevés horodatés.
- `Uptime` : aide à repérer un redémarrage récent ou un compteur réinitialisé.
- `log_error` ne garantit pas qu'un fichier local soit consultable.
- Une erreur proche de l'alerte n'établit pas la cause. Expurger IP, comptes et requêtes.

**Escalade :** heure, erreur, fréquence, évolution des compteurs et impact. Ne pas modifier les logs ni leur niveau de détail.

[Source : MySQL Server Status](https://dev.mysql.com/doc/refman/8.4/en/server-status-variables.html)
