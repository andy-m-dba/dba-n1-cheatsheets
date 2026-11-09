# MSSQL-N1-04 — Espace & fichiers

**Quand ?** Alerte stockage, fichier MDF/LDF volumineux, croissance inattendue.

### Taille allouée des fichiers (base courante)
```sql
SELECT name, type_desc,
       CAST(size * 8.0 / 1024 AS decimal(18,1)) AS taille_mo,
       physical_name
FROM sys.database_files;
```

**Exécuter dans la base ciblée** (sélectionner la bonne base dans SSMS). Ne pas exporter `physical_name` sur GitHub.

### Espace libre sur le serveur
Sur l'outil de supervision autorisé, relever les volumes des fichiers **DATA**, **LOG**, `tempdb` et sauvegardes.

### Lecture rapide
- `taille_mo` = taille **allouée**, pas espace réellement occupé ni espace libre du disque.
- Vérifier tendance et seuils internes ; une croissance peut être normale.
- Des fichiers `LOG` volumineux ne doivent **pas** être supprimés.

**Escalade :** volume, taux d'occupation, tendance, base et impact. Ne pas lancer `SHRINK`, supprimer de fichiers ou modifier `FILEGROWTH`.

[Source : sys.database_files](https://learn.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)
