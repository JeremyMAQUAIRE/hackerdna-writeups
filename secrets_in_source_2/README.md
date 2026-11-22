# Secrets in Source 2

**Lab :** [Secrets in Source 2 sur HackerDNA](https://hackerdna.com/labs/secrets-in-source-2)  
**Catégorie :** Sécurité web  
**Résultat :** Lab terminé

## Le clic droit est bloqué

Cette fois, le site du lab s'appelle **SecureVault Technologies**. Je voulais regarder son code HTML, comme dans le premier *Secrets in Source*, mais le clic droit était désactivé.

Ça complique un peu l'accès au menu « Afficher le code source », sans empêcher réellement de consulter le HTML.

J'ai donc saisi manuellement `view-source:` devant l'adresse du site, directement dans la barre d'adresse de Chrome :

```text
view-source:https://lab.hdna.me/145-secrets-in-source-2/
```

Le code source s'est affiché normalement.

## Le commentaire qui attire l'attention

Au début du `<body>`, j'ai repéré un commentaire `TODO` destiné à l'équipe DevOps. Il mentionnait un fichier texte qui était encore **world-readable**, autrement dit lisible publiquement.

Le commentaire donnait aussi son emplacement. Je masque ce chemin ici pour ne pas dévoiler la solution.

À partir de cet indice, j'ai vérifié dans le navigateur si le fichier était accessible. C'était bien le cas, et j'ai pu terminer le lab.

## Ce que ça montre

Bloquer le clic droit ne protège pas le code source. Le navigateur a besoin de recevoir le HTML pour afficher la page ; l'utilisateur peut donc le consulter autrement.

Le vrai problème était ailleurs : un commentaire de développement divulguait une information utile, et un fichier sensible restait accessible publiquement.

Pour éviter ce genre de situation sur un site réel, il faut retirer les informations internes du HTML, mais aussi protéger les ressources côté serveur. Une restriction dans l'interface ne remplace pas un contrôle d'accès.

## Ce que je retiens

J'ai trouvé ce deuxième exercice intéressant parce qu'il ajoute un petit obstacle au début. La manipulation à retenir est surtout la saisie manuelle de `view-source:`.

Ça confirme qu'il ne faut pas confondre une fonctionnalité désactivée dans le navigateur avec une vraie mesure de sécurité.

[Retour à la liste des labs](../README.md)
