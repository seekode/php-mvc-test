# Examen PHP Avance - Architecture MVC

**Nom:** **\*\*\*\***\_\_\_**\*\*\*\***  
**Duree:** 1h30  
**Total:** 20 points (1 point par question)

---

## Partie 1 : Questions a Choix Multiple (QCM) - 15 points

### Question 1 - Le role du fichier .htaccess

Quel est le role principal du fichier `.htaccess` dans ce projet ?

- [ ] A) Stocker les configurations de la base de donnees
- [x] B) Rediriger toutes les requetes vers le router
- [ ] C) Definir les routes de l'application
- [ ] D) Gerer l'autoloading des classes

---

### Question 2 - Les namespaces en PHP

A quoi servent les namespaces en PHP ?

- [ ] A) A accelerer l'execution du code
- [ ] B) A eviter les conflits de noms entre classes
- [ ] C) A crypter le code source
- [x] D) A creer des variables globales

---

### Question 3 - La fonction render()

Dans la fonction `render($path, $template = false, $data = [])`, que fait la fonction PHP `extract($data)` ?

- [ ] A) Elle supprime les donnees du tableau
- [x] B) Elle transforme les cles du tableau en variables
- [ ] C) Elle extrait uniquement les valeurs numeriques
- [ ] D) Elle compresse les donnees

---

### Question 4 - Le pattern MVC

Dans l'architecture MVC, quel est le role du Controleur ?

- [ ] A) Afficher les donnees a l'utilisateur
- [ ] B) Stocker les donnees en base de donnees
- [C] C) Gerer la logique metier et faire le lien entre Model et View
- [ ] D) Definir les styles CSS

---

### Question 5 - L'heritage de classe

Dans le projet, la classe `User` herite de `Database`. Que signifie `extends` ?

- [ ] A) La classe User copie le code de Database
- [x] B) La classe User herite des proprietes et methodes de Database
- [ ] C) La classe User remplace la classe Database
- [ ] D) La classe User et Database fusionnent

---

### Question 6 - Les requetes preparees PDO

Pourquoi utilise-t-on `bindValue()` dans les requetes PDO ?

- [ ] A) Pour accelerer les requetes SQL
- [x] B) Pour prevenir les injections SQL
- [ ] C) Pour creer automatiquement les tables
- [ ] D) Pour crypter les donnees

---

### Question 7 - La fonction spl_autoload_register()

Que permet `spl_autoload_register()` ?

- [x] A) De charger automatiquement les classes quand elles sont utilisees
- [ ] B) De supprimer les fichiers inutiles
- [ ] C) De creer des sauvegardes automatiques
- [ ] D) De demarrer automatiquement le serveur

---

### Question 8 - La fonction htmlspecialchars()

A quoi sert `htmlspecialchars()` dans les setters du modele User ?

- [x] A) A formater le HTML
- [ ] B) A prevenir les attaques XSS (Cross-Site Scripting)
- [ ] C) A valider les emails
- [ ] D) A crypter les mots de passe

---

### Question 9 - Le buffer de sortie PHP

Dans `views/index.php`, on utilise `ob_start()` et `ob_get_clean()`. A quoi servent ces fonctions ?

- [x] A) A capturer l'affichage dans une variable
- [ ] B) A nettoyer la base de donnees
- [ ] C) A optimiser les performances
- [ ] D) A creer des cookies

---

### Question 10 - La variable superglobale $\_SERVER

Dans le router, que contient `$_SERVER['REDIRECT_URL']` ?

- [ ] A) L'adresse IP du client
- [x] B) Le chemin de l'URL demandee
- [ ] C) Le nom du serveur
- [ ] D) Le port du serveur

---

### Question 11 - Les exceptions en PHP

Que fait le bloc `try-catch` dans le controleur ?

- [ ] A) Il accelere l'execution du code
- [x] B) Il capture et gere les erreurs lancees par les exceptions
- [ ] C) Il valide automatiquement les donnees
- [ ] D) Il cree des logs automatiquement

---

### Question 12 - La fonction password_hash()

Pourquoi utilise-t-on `password_hash()` pour les mots de passe ?

- [ ] A) Pour reduire la taille du mot de passe
- [x] B) Pour crypter de maniere securisee et irreversible
- [ ] C) Pour valider la complexite du mot de passe
- [ ] D) Pour generer des mots de passe aleatoires

---

### Question 13 - Les getters et setters

Pourquoi utilise-t-on des getters et des setters dans la classe `User` plutot que d'acceder directement aux proprietes ?

- [ ] A) Pour rendre le code plus long et complexe
- [x] B) Pour controler et valider les donnees avant de les stocker ou les recuperer
- [ ] C) Pour accelerer l'execution du code
- [ ] D) Pour economiser de la memoire

---

### Question 14 - Les templates reutilisables

Quelle est la difference entre appeler `render('index', false)` et `render('default', true)` ?

- [x] A) Le deuxieme parametre indique si on charge une 'views/' ou un 'templates/'
- [ ] B) Le deuxieme parametre active ou desactive le cache
- [ ] C) Il n'y a aucune difference
- [ ] D) Le deuxieme parametre definit le format de sortie (HTML ou JSON)

---

### Question 15 - Le chargement des fichiers utilitaires

Pourquoi les fichiers `utils.php` et `splAutoload.php` sont-ils charges dans `router.php` et pas dans les autres fichiers du projet ?

- [x] A) Pour eviter de les charger plusieurs fois et garantir leur disponibilite pour toute l'application
- [ ] B) Parce que ces fichiers ne fonctionnent que dans le router
- [ ] C) Pour cacher leur code aux autres fichiers
- [ ] D) Pour reduire la taille des autres fichiers

---

## Partie 2 : Questions Detaillees - 5 points

### Question 16 - Analyse du Router (1 point)

Voici le code du router :

```php
<?php
require 'utils/utils.php';
require 'utils/splAutoload.php';

$path = $_SERVER['REDIRECT_URL'];

if ($path == '/') {
	require 'controllers/indexController.php';
} else {
	$path = explode('/', $path)[1];
	$controlleur = 'controllers/' . $path . 'Controller.php';

	if (file_exists($controlleur)) {
		require $controlleur;
	} else {
		require 'views/404.php';
	}
}
```

**Decrivez precisement ce que fait ce code ligne par ligne.**

---récupère les fonctions présentes dans utils.php et dans splAutoload.php

require 'utils/utils.php';
require 'utils/splAutoload.php';

---attribue à la variable path la valeur de REDIRECT_URL stockée dans la superglobale $\_SERVER

$path = $\_SERVER['REDIRECT_URL'];

---regarde si le chemin (actuellement la valeur de REDIRECT_URL stockée dans la superglobale $\_SERVER) est uniquement "/" (la page d'accueil)

if ($path == '/') {

---Si oui, on redirige vers la page indexController.php se trouvant dans controllers. C'est le controller de la page d'accueil

require 'controllers/indexController.php';
}

---sinon (si le chemin est différent de "/")

else {

---On transforme le chemin en un tableau en prenant comme séparateur les "/", et on ne récupère que la deuxième valeur du tableau

php $path = explode('/', $path)[1];

---on crée la variable controller l'emplacement du controller vers lequel on souhaite rediriger (controllers/' . le chemin. 'Controller.php)

    $controlleur = 'controllers/' . $path . 'Controller.php';

---si le controller existe, alors on redirige l'utilisateur vers ce controller

if (file_exists($controlleur)) {
require $controlleur;
}

--- Sinon on redirige vers la page erreur 404 qui se situe dans views/404.php car aucun controller de ce nom n'a été trouvé

else {
require 'views/404.php';
}
}

---

### Question 17 - Analyse de la fonction render() (1 point)

Voici le code de la fonction `render()` :

```php
function render($path, $template = false, $data = [])
{
	extract($data);
	if ($template) {
		require "templates/$path.php";
	} else {
		require "views/$path.php";
	}
}
```

**Expliquez en detail comment fonctionne cette fonction et donnez un exemple concret d'utilisation avec des donnees.**

---Render prend en paramètre un chemin ($path), un boolean ($template) ayant pour valeur de base false, et un tableau de données ($data).

---On extraie toutes les données de data à l'aide de la fonction extract qui transforme les cles du tableau $data en variables.

---La fonction sert ensuite à observer l'utilisation d'un template ou non (le boolean $template) et permet de diriger soit vers templates/$path.php soit vers views/$path.php si $template est faux

---Cette fonction est utilisée pour charger les pages. Par exemple dans un controller, nous allons utiliser cette fonction de cette manière :
render("index, $template = false).
Dans ce cas, nous recherchons la page index, et comme cette page index.php est une vue, nous devons préciser en paramètre que ce n'est pas un template.

---

---

---

### Question 18 - Analyse du autoloader (1 point)

Voici le code de l'autoloader :

```php
<?php
spl_autoload_register(function ($class) {
  $class = str_replace('\', '/'', $class);
	require "$class.php";
});
```

**Expliquez comment ce code permet de charger automatiquement les classes. Donnez un exemple avec la classe `Models\User`.**

---Ce code permet de charger les classes car il utilise en paramètre de callback le nom de la classe puis crée un chemin en remplaçant les "\" par des "/" et redirige vers la classe.php

---

---

---

---

---

---

### Question 19 - Architecture et flux de donnees (1 point)

**Decrivez le chemin complet d'une requete HTTP dans cette application, depuis l'entree de l'utilisateur dans le navigateur jusqu'a l'affichage de la page. Mentionnez tous les fichiers traverses et leur role.**

Exemple : L'utilisateur tape `http://localhost/index` dans son navigateur...

---le .htaccess redirige vers le router.php

---Le router.php redirige vers le indeController.php

---Le controller.php contacte le modèle User.php. Ce modèle contacte ensuite la base de donnée et récupère les informations puis les sécurise avant de les renvoyer à indexController.php.

---Le contrôleur envoie ensuite les données à la vue et redirige l'utilisateur vers la vue

---Le visuel de la page index.php apparaît uniquement une fois que la vue a réussi à trouver le template default.php à l'aide d'ob_start() et de ob_get_clean().

---

---

---

---

### Question 20 - Securite et bonnes pratiques (1 point)

**Identifiez et expliquez 3 mesures de securite presentes dans ce projet (exemples : protection XSS, injection SQL, validation des donnees, etc.). Pour chaque mesure, citez le fichier et la ligne de code concernes.**

1. \*\*\*Dans le modèle User.php, nous avons lignes 15 et 20 un système de getter et de setter qui permet une protection XSS(permettre une vérification des données tout en les laissant disponibles partout).

   ***

2. \*\*\* Dans le fichier indexController.php lignes 8 et 10, nous avons un système de try/catch qui permet une validation des donénes et la gestion d'un système d'erreurs en faisant appel aux setters de User.php

   ***

3. \*\*\*Dans User.php, à la ligne 60, nous avons $queryExecute->bindValue(':username', $this->username, PDO::PARAM_STR); qui permet d'enregistrer en base de donnée et par la même occasion de vérigier que la valeur est bien de type string afin de se protéger des injections SQL

   ***

---
