# 🔐 HackerDNA — 3. Secrets in Source 2

![Category](https://img.shields.io/badge/Catégorie-Web%20Security-blue)
![Difficulty](https://img.shields.io/badge/Difficulté-Débutant-green)
![Status](https://img.shields.io/badge/Statut-Résolu-brightgreen)

## 📋 Présentation

Ce write-up présente ma démarche sur le laboratoire **Secrets in Source 2** proposé par HackerDNA.

- **Plateforme :** [HackerDNA](https://hackerdna.com)
- **Challenge :** [Secrets in Source 2](https://hackerdna.com/labs/secrets-in-source-2)
- **Lien direct :** https://hackerdna.com/labs/secrets-in-source-2
- **Catégorie :** Web Security
- **Statut :** ✅ Résolu

> ⚠️ Aucun flag réel, identifiant sensible ou chemin secret complet n'est divulgué dans ce compte rendu.

## 🎯 Objectif

Le laboratoire propose une application web vitrine fictive intitulée **SecureVault Technologies — Enterprise Security Solutions**.

L'objectif est d'examiner les informations exposées par le site et de comprendre comment une indication laissée dans le code source peut mener à une ressource qui n'aurait pas dû être publique.

## 🔎 Étape 1 — Reconnaissance

Après avoir ouvert l'application, j'ai cherché à afficher son code source HTML. Le **clic droit est bloqué**, ce qui empêche d'utiliser le menu contextuel habituel pour sélectionner « Afficher le code source de la page ».

Cette restriction ne protège pas le HTML envoyé au navigateur.

### Contourner le blocage du clic droit

Dans la barre d'adresse de Chrome, j'ai saisi **manuellement** le préfixe suivant devant l'URL de l'application :

```text
view-source:https://lab.hdna.me/145-secrets-in-source-2/
```

Il est important de **taper `view-source:` directement** dans la barre d'adresse, plutôt que de dépendre du menu contextuel bloqué.

Le navigateur affiche alors le HTML brut de la page.

## 🧩 Étape 2 — Examiner les commentaires HTML

Au début de la section `<body>`, un commentaire HTML de type `TODO` attire l'attention :

```html
<!-- TODO(devops): /[CHEMIN_MASQUÉ]/flag.txt is still world-readable, lock it down before launch -->
```

Ce commentaire donne deux indices importants :

1. Une ressource texte sensible existe à un emplacement indiqué dans le HTML.
2. La mention **`world-readable`** suggère qu'elle est lisible publiquement, sans restriction d'accès appropriée.

Le chemin exact est volontairement masqué ici pour ne pas gâcher le défi.

## 🚀 Étape 3 — Vérifier l'exposition de la ressource

À partir de l'indice présent dans le commentaire, j'ai testé l'accès à la ressource depuis la barre d'adresse du navigateur.

Exemple **schématique**, sans révéler le chemin du laboratoire :

```text
https://<hôte-du-laboratoire>/[CHEMIN_MASQUÉ]/flag.txt
```

La ressource répond directement dans le navigateur, ce qui confirme le problème d'exposition décrit par le commentaire.

> 🔒 Le contenu du fichier, le flag et le chemin réel ne sont pas reproduits.

## 🛡️ Analyse de la vulnérabilité

### Type de vulnérabilité

**Information Disclosure — Divulgation d'informations sensibles**

Deux faiblesses se cumulent :

- **Fuite d'information dans le code HTML :** un commentaire destiné aux développeurs révèle l'existence et l'emplacement d'une ressource sensible.
- **Contrôle d'accès insuffisant :** la ressource est accessible publiquement côté serveur.

Le blocage du clic droit ne constitue **pas une mesure de sécurité** : le navigateur reçoit toujours le code HTML, et d'autres méthodes permettent de le consulter.

### Recommandations

- Retirer les commentaires internes sensibles avant la mise en production.
- Ne jamais placer de secrets dans les ressources web publiques.
- Stocker les fichiers confidentiels hors de la racine publique du serveur.
- Appliquer une authentification et une autorisation côté serveur lorsque nécessaire.
- Vérifier régulièrement les ressources accessibles sans authentification.
- Ne pas considérer la désactivation du clic droit comme une protection.

## 🧰 Outils utilisés

| Outil | Utilisation |
|---|---|
| Google Chrome | Navigation dans l'application |
| `view-source:` | Affichage du HTML malgré le blocage du clic droit |
| Analyse HTML | Identification du commentaire `TODO` |
| Barre d'adresse | Vérification de l'accès à la ressource |

## 📚 Ce que j'ai appris

Ce laboratoire m'a permis de comprendre :

- Comment afficher le code source même lorsque le clic droit est désactivé.
- Pourquoi les commentaires HTML sont visibles par les visiteurs.
- Comment une note de développement peut exposer un chemin sensible.
- Pourquoi la sécurité des fichiers doit être assurée **côté serveur**.

## ✅ Conclusion

Le laboratoire **Secrets in Source 2** montre qu'un blocage d'interface, comme la désactivation du clic droit, ne protège pas les informations transmises au navigateur.

Une simple consultation du code source a permis de repérer un commentaire de développement, puis de constater l'exposition d'une ressource sensible.

**Statut : Challenge résolu ✅**

---

**Auteur :** [JeremyMAQUAIRE](https://github.com/JeremyMAQUAIRE)

**Repository :** [hackerdna-writeups](https://github.com/JeremyMAQUAIRE/hackerdna-writeups)

**Laboratoire officiel :** [Secrets in Source 2](https://hackerdna.com/labs/secrets-in-source-2)

> Documentation réalisée dans un cadre pédagogique et de cybersécurité éthique, sans divulgation de flag ni de secret.
