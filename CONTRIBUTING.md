# Contribution aux CheatSheets N1

Une fiche = un objectif de diagnostic. Rédiger en français, conserver les commandes et noms de vues en anglais.

## Plan obligatoire

1. Symptômes et objectif
2. Versions, architecture, prérequis et droits
3. Commandes **non destructives**
4. Interprétation : normal, suspect, ambigu, valeurs NULL et vues vides
5. Informations à transmettre
6. Critères d'escalade N2/N3
7. Actions interdites sans autorisation
8. Documentation officielle

## Checklist

- [ ] Aucun secret, log brut, nom de serveur ou IP interne
- [ ] SQL et commandes relus pour la version ciblée
- [ ] Privilèges et limitations indiqués
- [ ] Interprétation contextualisée ; hypothèses non présentées comme causes
- [ ] Pas de commande modifiant données, service, paramètres ou rôles
- [ ] Test en environnement de référence documenté, ou **Non testé** indiqué
- [ ] Revue documentaire distinguée des tests d'exécution
- [ ] Revue technique N2/N3 et tests adaptés avant passage au statut **Validé**

Les seuils et niveaux de sévérité restent ceux de l'organisation. Les changements passent par Pull Request.
