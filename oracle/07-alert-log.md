# ORA-N1-07 — Alert log : erreurs récentes

**Quand ?** Erreur ORA répétée, arrêt inexpliqué, alerte sans cause visible.

### Alert log via SQL (avec droits adaptés)
```sql
SELECT originating_timestamp, message_text
FROM v$diag_alert_ext
WHERE originating_timestamp >= SYSTIMESTAMP - INTERVAL '1' HOUR
  AND message_type IN (2,3,4)
ORDER BY originating_timestamp DESC
FETCH FIRST 20 ROWS ONLY;
```

### Lecture rapide
- Types `2` = incident, `3` = erreur, `4` = avertissement.
- Une alerte récente n'est **pas forcément** la cause de l'incident métier.
- Les messages peuvent contenir des noms, chemins ou informations sensibles : **expurger** avant partage.
- Vue accessible selon les privilèges et le conteneur ; aucun résultat peut simplement signifier aucune alerte de ces types sur la dernière heure.

**Escalade :** heure, code ORA, fréquence, contexte et impact. Ne pas supprimer traces ni modifier l'ADR.

[Source : V$DIAG_ALERT_EXT](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/V-DIAG_ALERT_EXT.html)
