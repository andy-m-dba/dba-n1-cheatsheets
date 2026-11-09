# PG-N1-00 — Triage initial (5 minutes)

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Objectif

Qualifier « PostgreSQL inaccessible / lent / alerte » sans modifier le service.

## 1. Noter les faits

Heure et fuseau, alerte exacte, service concerné, étendue de l'impact métier, identité de l'instance dans les outils internes et changements récents connus. Ne rien publier de sensible.

## 2. Disponibilité du serveur

```bash
pg_isready -h HOTE_EXEMPLE -p 5432 -d BASE_EXEMPLE -U UTILISATEUR_LECTURE
echo $?
```

| Code | Interprétation |
|---|---|
| `0` | Serveur accepte les connexions ; ne prouve pas que l'application fonctionne |
| `1` | Connexions refusées par le serveur, parfois transitoires |
| `2` | Aucune réponse obtenue |
| `3` | Paramètres incorrects / test non effectué |

`pg_isready` ne valide ni la réussite de l'authentification, ni le fonctionnement de l'application. Des paramètres erronés peuvent créer des entrées d'échec dans les journaux ; utiliser les paramètres inventoriés et autorisés.

## 3. Si connexion SQL autorisée

```sql
SELECT now() AS heure_serveur,
       current_database() AS base,
       current_user AS compte,
       pg_is_in_recovery() AS est_standby,
       pg_postmaster_start_time() AS demarrage;

SELECT state, count(*) AS nb
FROM pg_stat_activity
GROUP BY state
ORDER BY nb DESC;
```

Les données de `pg_stat_activity` sont partiellement masquées sans privilèges statistiques suffisants. Une mesure unique ne permet pas de conclure sur une tendance.

## 4. Orienter le diagnostic

- Connexion en échec : [01 — Connexion](01-connexion-version.md).
- Nombre inhabituel de sessions ou lenteur : [02 — Sessions](02-sessions-verrous.md).
- Alerte disque : [03 — Espace](03-espace-capacite.md).
- Alerte standby : [04 — Réplication](04-replication.md).
- Alerte backup / WAL : [05 — WAL](05-wal-sauvegardes.md).

## Escalade

Indisponibilité, risque de perte de données, saturation ou impact métier majeur : ouvrir un ticket immédiatement selon la matrice locale. [Modèle de ticket](06-escalade.md).

**Ne pas** redémarrer, purger WAL, terminer des sessions ni déclencher une bascule.

**Source :** [pg_isready](https://www.postgresql.org/docs/current/app-pg-isready.html).
