# 🔐 HackerDNA — 2. Secrets in Source

![Category](https://img.shields.io/badge/Catégorie-Web%20Security-blue)
![Difficulty](https://img.shields.io/badge/Difficulté-Débutant-green)
![Status](https://img.shields.io/badge/Statut-Résolu-brightgreen)

## 📋 Présentation

Ce write-up présente la résolution du laboratoire **Secrets in Source** proposé par HackerDNA.

- **Plateforme :** [HackerDNA](https://hackerdna.com)
- **Challenge :** [Secrets in Source](https://hackerdna.com/labs/secrets-in-source)
- **Lien direct :** https://hackerdna.com/labs/secrets-in-source
- **Catégorie :** Web Security
- **Statut :** ✅ Résolu

> ⚠️ Les informations sensibles, chemins secrets et flags sont volontairement masqués.

## 🎯 Objectif

Le laboratoire met à disposition un site vitrine fictif nommé **TechNova Solutions**.

L'objectif est d'analyser les ressources accessibles depuis le navigateur afin de retrouver une information sensible oubliée par un développeur.

## 🔎 Étape 1 — Reconnaissance

Après avoir ouvert l'application web, j'ai commencé par examiner les différentes sections du site.

La section de contact contient un indice invitant à regarder ce qui se trouve « sous le capot » du site.

J'ai donc décidé d'inspecter le code source HTML.

### Affichage du code source

Dans Google Chrome, j'ai utilisé le raccourci :

```text
Ctrl + U
```

Cette manipulation permet d'afficher le code HTML envoyé par le serveur.

## 🧩 Étape 2 — Analyse du code HTML

En parcourant le code source, j'ai remarqué deux commentaires HTML intéressants vers les lignes 105 et 106.

```html
<!-- Dev note: launch checklist passed, marketing copy approved. -->
<!-- TODO: move the flag "/[REDACTED]/flag.txt" to a more secure location -->
```

Le second commentaire révèle qu'un fichier nommé `flag.txt` est présent sur le serveur.

Son emplacement est directement indiqué dans le code source, ce qui constitue une divulgation d'information.

## 🚀 Étape 3 — Accès au fichier

À partir du chemin découvert dans le commentaire HTML, j'ai construit une URL en ajoutant ce chemin à l'adresse du laboratoire.

```text
https://lab.hdna.me/4-secrets-in-source/[REDACTED]/flag.txt
```

J'ai ensuite ouvert cette adresse directement dans le navigateur.

Le serveur a retourné le contenu du fichier texte sans demander d'authentification.

## 🏁 Étape 4 — Récupération du flag

Le fichier contenait une valeur correspondant au flag attendu par le laboratoire.

```text
FLAG: [REDACTED]
```

Le flag a été récupéré avec succès.

> 🔒 Le flag réel n'est pas publié afin de préserver l'intérêt pédagogique du challenge.

## 🛡️ Analyse de la vulnérabilité

### Type de vulnérabilité

**Information Disclosure — Divulgation d'informations sensibles**

Deux problèmes sont identifiables :

1. **Commentaire HTML sensible :** un développeur a laissé dans le code source un commentaire révélant l'emplacement d'un fichier.
2. **Fichier publiquement accessible :** le fichier contenant le flag peut être consulté sans authentification.

### Pourquoi est-ce dangereux ?

Les commentaires HTML ne sont pas affichés directement sur la page, mais ils sont accessibles à tous les visiteurs qui consultent son code source.

Ils peuvent révéler des chemins internes, des fichiers confidentiels ou des informations utiles à un attaquant.

### Recommandations

- Supprimer les commentaires sensibles avant la mise en production.
- Ne jamais stocker de secrets dans les fichiers publics.
- Placer les ressources confidentielles hors du répertoire web accessible.
- Mettre en place des contrôles d'accès adaptés.
- Vérifier les fichiers exposés lors des audits de sécurité.

## 🧰 Outils utilisés

| Outil | Utilisation |
|---|---|
| Google Chrome | Navigation sur le site |
| Ctrl + U | Affichage du code source |
| Analyse HTML | Identification des commentaires |
| Barre d'adresse | Accès au fichier découvert |

## 📚 Ce que j'ai appris

Ce laboratoire m'a permis de comprendre :

- L'importance de consulter le code source HTML.
- Les risques liés aux commentaires laissés par les développeurs.
- La manière dont un chemin exposé peut conduire à un fichier sensible.
- L'importance de protéger les ressources côté serveur.

## ✅ Conclusion

Le challenge **Secrets in Source** démontre qu'une simple analyse du code HTML peut permettre de découvrir des informations sensibles.

Aucun outil complexe n'a été nécessaire : le navigateur, l'affichage du code source et l'analyse des commentaires ont suffi.

**Statut : Challenge résolu ✅**

---

**Auteur :** [JeremyMAQUAIRE](https://github.com/JeremyMAQUAIRE)

**Repository :** [hackerdna-writeups](https://github.com/JeremyMAQUAIRE/hackerdna-writeups)

> Documentation réalisée dans un cadre pédagogique et de cybersécurité éthique.

