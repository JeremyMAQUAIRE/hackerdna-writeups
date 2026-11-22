# Secrets in Source

**Lab :** [Secrets in Source sur HackerDNA](https://hackerdna.com/labs/secrets-in-source)  
**Catégorie :** Sécurité web  
**Résultat :** Lab terminé

## Un indice dans le code HTML

Le lab présente un site vitrine fictif, **TechNova Solutions**. Au premier abord, rien de très particulier : on peut naviguer sur le site et lire son contenu.

Dans la partie contact, un indice invite à regarder « sous le capot ». J'ai donc ouvert le code source de la page avec **Ctrl + U** dans Chrome.

En parcourant le HTML, je suis tombé sur des commentaires laissés par les développeurs, vers les lignes 105 et 106. L'un d'eux évoquait un fichier qui aurait dû être déplacé vers un emplacement plus sûr.

Je ne reproduis pas le commentaire complet, puisqu'il contient le chemin utilisé pour résoudre le défi. Ce qui compte ici, c'est qu'un simple commentaire HTML révélait l'existence d'un fichier sensible.

## Vérifier l'indice

À partir du chemin indiqué dans le commentaire, j'ai testé l'accès à la ressource dans la barre d'adresse du navigateur.

Le fichier était accessible directement, sans demande d'authentification. J'ai ainsi pu terminer le lab.

Je ne mets ni l'URL complète du fichier ni son contenu pour laisser la possibilité de chercher par soi-même.

## Pourquoi c'est un problème

Un commentaire HTML n'apparaît pas sur la page telle qu'on la voit normalement, mais il est envoyé au navigateur avec le reste du code. N'importe quel visiteur peut donc le consulter.

Ici, deux choses se cumulaient : un commentaire révélait où chercher et le serveur laissait accéder au fichier.

Sur un vrai site, il faudrait éviter de laisser des chemins sensibles dans le HTML et surtout empêcher l'accès public aux fichiers qui ne doivent pas l'être. Supprimer le commentaire ne suffirait pas à sécuriser la ressource.

## Ce que je retiens

Ce lab m'a montré l'intérêt de commencer par des vérifications simples. Pas besoin d'un scanner ou d'un outil complexe : le code source et la barre d'adresse ont suffi.

[Retour à la liste des labs](../README.md)
