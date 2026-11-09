# MYSQL-N1-05 — Sauvegardes

**Quand ?** Job en échec, backup absent ou alerte RPO.

### Vérifier dans l'outil autorisé (lecture seule)
- `mysqldump` / `mariadb-dump` : ordonnanceur, heure et statut.
- `mysqlbackup` / `mariadb-backup` : console ou rapports de sauvegarde.
- Snapshots / service managé : tableau de bord prévu par l'organisation.
- Pour le PITR, contrôler **l'état déclaré** des journaux nécessaires, sans les manipuler.

### Lecture rapide
- Comparer le dernier succès et la fréquence au **RPO** attendu.
- Job `success` ≠ sauvegarde restaurable : seul un test de restauration l'atteste.
- L'historique incomplet d'un outil ne prouve pas l'absence de toute sauvegarde.
- La capacité à restaurer dans le temps prévu dépend aussi du **RTO**.

**Escalade :** base, outil, type, dernier succès, échec expurgé et objectif concerné. Aucun backup forcé, `RESTORE` ou purge de binlogs N1.

[Sources : MySQL](https://dev.mysql.com/doc/refman/8.4/en/backup-and-recovery.html) · [MariaDB](https://mariadb.com/docs/server/server-usage/backup-and-restore/)
