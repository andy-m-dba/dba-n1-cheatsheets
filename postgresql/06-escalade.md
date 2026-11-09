# PG-N1-06 — Escalade et ticket

**Niveau :** N1 · **Statut :** Brouillon · **Revue documentaire :** 2026-11-09 · **Test réel :** Non

## Quand escalader ?

- Indisponibilité / impact métier / risque de perte de données.
- Stockage saturé ou évolution inquiétante.
- Réplica attendu absent ou retard supérieur au seuil local.
- Blocages persistants et impact applicatif.
- Sauvegarde en échec ou objectifs de sauvegarde compromis.
- Privilèges insuffisants ou résultat ambigu empêchant de conclure.

Les seuils, SLA et niveaux de sévérité sont définis par l'organisation.

## Ticket d'incident (canal interne, sans secrets)

```text
Titre : [PostgreSQL][ENV][SERVICE] Symptôme observable
Heure et fuseau : AAAA-MM-JJ HH:MM TZ
Criticité proposée : selon matrice interne
Impact métier / utilisateurs : ...
Instance / cluster : référence interne seulement
Rôle observé : primaire / standby / inconnu
Version PostgreSQL : ...
Message d'erreur expurgé : ...
Observations N1 :
- pg_isready : code, heure
- Connexion SQL : OK / KO / raison
- Sessions / blocages : résumé quantifié
- Disque / inodes : volume et tendance
- Réplication / backup : attendu versus observé
Changements récents connus : ...
Limites du diagnostic (droits, résultats masqués, contrôles impossibles) : ...
Hypothèses non confirmées : ...
Actions N1 : diagnostics non destructifs
Demande au N2/N3 : ...
Pièces jointes : sorties expurgées
```

## Après prise en charge

Suivre la supervision et la confirmation applicative avant de conclure au rétablissement ; `pg_isready` ne suffit pas. Conserver la RCA uniquement après validation N2/N3.

**Ne pas** fermer un incident critique sur une hypothèse non confirmée.
