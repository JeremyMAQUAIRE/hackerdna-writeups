# 🔐 HackerDNA — 4. Hack the Login

![Category](https://img.shields.io/badge/Catégorie-Web%20Security-blue)
![Difficulty](https://img.shields.io/badge/Difficulté-Débutant-green)
![Status](https://img.shields.io/badge/Statut-Résolu-brightgreen)

## 📋 Présentation

Ce write-up présente la résolution du laboratoire **Hack the Login** proposé par HackerDNA.

- **Plateforme :** [HackerDNA](https://hackerdna.com)
- **Challenge :** [Hack the Login](https://hackerdna.com/labs/hack-the-login)
- **Lien direct :** https://hackerdna.com/labs/hack-the-login
- **Catégorie :** Web Security
- **Statut :** ✅ Résolu

> ⚠️ Les identifiants, mots de passe, chemins sensibles et flags sont volontairement omis pour préserver l'intérêt du défi.

## 🎯 Objectif

Le laboratoire présente une page de connexion intitulée **Access Restricted**. Un message explique qu'il s'agit d'un exercice de hacking et que les informations permettant de se connecter sont cachées dans le code de la page.

L'objectif est d'analyser les ressources publiques du site afin de comprendre le mécanisme d'authentification et d'accéder à l'interface protégée dans le cadre du laboratoire.

## 🔎 Étape 1 — Reconnaissance

Après avoir ouvert l'application web, j'ai observé un formulaire classique comportant :

- Un champ **Username**.
- Un champ **Password**.
- Un bouton **Login**.

Le texte d'introduction indique que la solution se trouve dans le code de la page. J'ai donc choisi d'examiner le code source HTML plutôt que d'essayer des identifiants au hasard.

### Affichage du code source

Dans Google Chrome, le raccourci suivant permet d'afficher le HTML :

```text
Ctrl + U
```

Il est également possible d'utiliser le préfixe `view-source:` devant l'adresse de la page.

## 🧩 Étape 2 — Identifier le fichier JavaScript

Vers la fin du document HTML, j'ai repéré une référence à un fichier JavaScript externe :

```html
<script src="script.js"></script>
```

Le HTML contient aussi un script lié au comportement du formulaire et à l'affichage d'un message d'aide. Le fichier externe constitue une piste plus intéressante pour comprendre le traitement de la connexion.

J'ai ouvert `script.js` dans le navigateur afin de lire son contenu.

## 🔍 Étape 3 — Analyser le mécanisme d'authentification

Dans le JavaScript, un gestionnaire d'événement intercepte l'envoi du formulaire :

```javascript
document.getElementById('loginForm').addEventListener('submit', function(e) {
  e.preventDefault();
  // Lecture et vérification des champs de connexion
});
```

Le script lit les valeurs des champs, supprime les espaces inutiles avec `trim()`, puis les compare à des **valeurs codées en dur dans le JavaScript**.

Le problème est que ce fichier est téléchargé par le navigateur : tout visiteur peut donc examiner la logique d'authentification et les informations qui y figurent.

> 🔒 Les valeurs de connexion réelles ne sont pas reproduites dans ce write-up.

## 🚀 Étape 4 — Valider la connexion

Après avoir compris la logique du script, j'ai utilisé le formulaire dans l'environnement autorisé du laboratoire.

La connexion réussie affiche le message **Access granted** et indique que l'utilisateur est connecté avec des privilèges administrateur.

Le code JavaScript prévoit ensuite la récupération d'une ressource texte et l'affichage du résultat dans l'interface.

Le laboratoire affiche une section **User flag**, confirmant la réussite de l'exercice.

> 🔒 Aucun flag, chemin de récupération ou contenu de ressource sensible n'est publié.

## 🛡️ Analyse de la vulnérabilité

### Type de vulnérabilité

**Client-Side Authentication / Information Disclosure — Authentification côté client et divulgation d'informations**

Le principal défaut est de confier au JavaScript exécuté dans le navigateur la vérification des identifiants, avec des valeurs de référence codées en dur.

### Pourquoi est-ce dangereux ?

Le code JavaScript envoyé au navigateur est consultable par l'utilisateur. Il ne peut donc pas servir de coffre-fort pour des secrets.

Une interface qui annonce « Access granted » après une simple comparaison côté client ne constitue pas, à elle seule, une protection fiable des ressources du serveur.

### Recommandations

- Vérifier les identifiants **côté serveur**, jamais uniquement dans le navigateur.
- Ne jamais intégrer de mots de passe ou de secrets dans le JavaScript public.
- Stocker les mots de passe avec un algorithme de hachage adapté, comme Argon2id.
- Contrôler l'authentification et les autorisations pour chaque ressource protégée.
- Éviter de confondre une restriction d'interface avec un véritable contrôle d'accès.
- Vérifier les scripts et ressources publics avant toute mise en production.

## 🧰 Outils utilisés

| Outil | Utilisation |
|---|---|
| Google Chrome | Navigation et test du formulaire |
| `Ctrl + U` / `view-source:` | Consultation du code HTML |
| `script.js` | Analyse de la logique de connexion |
| Barre d'adresse | Ouverture du fichier JavaScript |
| Formulaire de connexion | Vérification du comportement de l'application |

## 📚 Ce que j'ai appris

Ce laboratoire m'a permis de comprendre :

- Comment retrouver les scripts JavaScript chargés par une page HTML.
- Pourquoi les fichiers JavaScript publics ne doivent pas contenir de secrets.
- Comment reconnaître une vérification d'identifiants effectuée côté client.
- La différence entre une validation visuelle du formulaire et une authentification sécurisée côté serveur.
- L'importance de protéger les ressources sensibles indépendamment de l'interface.

## ✅ Conclusion

Le laboratoire **Hack the Login** démontre les risques d'une authentification implémentée directement dans le JavaScript du navigateur.

En analysant le HTML, puis le script externe, il a été possible de comprendre la logique de connexion et de terminer le défi dans son environnement prévu.

**Statut : Challenge résolu ✅**

---

**Auteur :** [JeremyMAQUAIRE](https://github.com/JeremyMAQUAIRE)

**Repository :** [hackerdna-writeups](https://github.com/JeremyMAQUAIRE/hackerdna-writeups)

**Laboratoire officiel :** [Hack the Login](https://hackerdna.com/labs/hack-the-login)

> Documentation réalisée dans un cadre pédagogique et de cybersécurité éthique, sans divulgation d'informations critiques.
