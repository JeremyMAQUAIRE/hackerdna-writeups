# Hack the Login

**Lab :** [Hack the Login sur HackerDNA](https://hackerdna.com/labs/hack-the-login)  
**Catégorie :** Sécurité web  
**Résultat :** Lab terminé

## Une page de connexion un peu particulière

Le lab affiche une page **Access Restricted**, avec un formulaire classique : nom d'utilisateur, mot de passe et bouton de connexion.

Le texte de la page précise que les informations nécessaires se trouvent dans son code. Plutôt que d'essayer des identifiants au hasard, j'ai donc commencé par regarder le HTML.

## Du HTML au JavaScript

J'ai affiché le code source avec **Ctrl + U** dans Chrome.

Vers la fin du fichier, j'ai remarqué cette ligne :

```html
<script src="script.js"></script>
```

Elle indique que la page charge un fichier JavaScript externe. J'ai ouvert ce fichier dans le navigateur pour voir comment le formulaire était traité.

Le script contient un écouteur sur l'envoi du formulaire :

```javascript
document.getElementById('loginForm').addEventListener('submit', function(e) {
  e.preventDefault();
  // Le script lit ensuite les champs et vérifie leurs valeurs.
});
```

En continuant la lecture, j'ai constaté que la vérification des identifiants se faisait directement dans ce JavaScript, à partir de valeurs écrites dans le fichier.

C'est là que se trouvait le problème : ce fichier est public et son contenu peut être lu par n'importe quel visiteur. Je ne recopie pas les identifiants présents dans le script pour ne pas donner la réponse.

## Tester la connexion

Une fois le fonctionnement compris, j'ai renseigné le formulaire dans l'environnement du lab.

La page a affiché **Access granted**, avec une indication de connexion en tant qu'administrateur. Le script prévoyait également la lecture d'un fichier texte pour afficher le résultat attendu par l'exercice.

Le lab a bien été validé. Je laisse de côté le flag et le chemin du fichier concerné.

## Ce qui ne va pas dans cette authentification

Le problème n'est pas simplement que le JavaScript est visible : c'est normal pour du code exécuté dans le navigateur.

Le problème, c'est d'y avoir placé les informations servant à vérifier la connexion. Une comparaison effectuée uniquement côté client ne peut pas sécuriser une véritable application.

Dans un site en production, le serveur doit vérifier l'identité de l'utilisateur et contrôler l'accès aux ressources protégées. Les mots de passe ne doivent pas être intégrés dans les scripts envoyés au navigateur.

## Ce que je retiens

Ce lab m'a permis de faire le lien entre le HTML et les fichiers JavaScript qu'il charge. Une simple référence à `script.js` m'a orienté vers la logique de connexion.

Il m'a aussi rappelé une règle importante : **ce qui est envoyé au navigateur ne doit pas être considéré comme secret**.

[Retour à la liste des labs](../README.md)
