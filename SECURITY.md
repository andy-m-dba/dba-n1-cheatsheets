# Sécurité et confidentialité

Ce dépôt est destiné à des procédures génériques. **Aucune donnée de production ou client** ne doit y figurer.

- Ne jamais publier de mot de passe, token, `.pgpass`, clé privée, chaîne de connexion sensible, nom d'hôte ou IP interne.
- Ne pas copier de logs bruts, requêtes métier, exports de tables, détails réseau ou captures non anonymisées.
- Utiliser des placeholders fictifs et des comptes de diagnostic à privilèges minimaux.
- Ne pas contourner les droits de lecture.
- En cas de fuite, suivre immédiatement la procédure de signalement et de rotation/révocation : supprimer un fichier ne retire pas le secret de l'historique Git.

Le N1 documente et escalade : toute modification du service, du stockage ou des données nécessite procédure et autorisation explicites.
