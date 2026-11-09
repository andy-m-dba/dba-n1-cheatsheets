# DBA N1 — CheatSheets

Fiches opérationnelles de premier niveau pour la supervision et le diagnostic initial des bases de données.

> **Statut : brouillon technique.** Commandes documentées, non exécutées en environnement de référence. Toute fiche nécessite une validation N2/N3 avant utilisation en production.

## Objectif

**N1 : observer → qualifier → documenter → escalader.** Ce dépôt ne fournit pas d'actions correctives autonomes.

| Moteur | État | Documentation |
|---|---|---|
| PostgreSQL | Premier lot à valider | [Fiches PostgreSQL](postgresql/README.md) |
| SQL Server | À préparer | — |
| Oracle | À préparer | — |
| MongoDB | À préparer | — |

## Référentiels distincts

- **dba-n1-cheatsheets** : qualification initiale, contrôles non destructifs et escalade ;
- **dba-n2-cheatsheets** : investigation détaillée et corrections approuvées ;
- **dba-n3-cheatsheets** : expertise, incidents complexes, RCA, architecture et DBRE.

Les deux autres dépôts seront créés indépendamment.

## Règles N1

1. Utiliser exclusivement les accès et commandes approuvés.
2. Collecter les faits horodatés, les messages expurgés, le contexte et l'impact.
3. Comparer aux seuils validés localement : aucun seuil universel n'est présumé.
4. Remonter les anomalies à N2/N3, sans transformer les hypothèses en causes établies.
5. Ne pas redémarrer un service, interrompre des sessions, promouvoir un standby, modifier des données ou supprimer des fichiers.

**Confidentialité :** ne jamais committer de secret, nom d'hôte ou IP d'entreprise, requête métier ou log brut. Voir [SECURITY.md](SECURITY.md).

## Arborescence

```text
dba-n1-cheatsheets/
├── README.md
├── CONTRIBUTING.md
├── SECURITY.md
├── .gitignore
├── .github/pull_request_template.md
├── postgresql/
│   ├── README.md
│   ├── 00-triage-5-minutes.md
│   ├── 01-connexion-version.md
│   ├── 02-sessions-verrous.md
│   ├── 03-espace-capacite.md
│   ├── 04-replication.md
│   ├── 05-wal-sauvegardes.md
│   └── 06-escalade.md
└── templates/
    └── fiche-n1.md
```

## Contribuer

Suivre [CONTRIBUTING.md](CONTRIBUTING.md), proposer les modifications via Pull Request et conserver le statut **Brouillon** tant qu'aucune revue N2/N3 et aucun test adapté n'ont eu lieu.

**Revue documentaire initiale :** 2026-11-09. Une revue technique documentaire complémentaire est proposée en [Pull Request](https://github.com/andy-m-dba/dba-n1-cheatsheets/pulls). **Validation N2/N3 et tests d'exécution : non réalisés.**
