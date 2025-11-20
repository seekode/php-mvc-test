# Examen PHP Avance - Architecture MVC

**Nom:** ___________________  
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
- [x] B) A eviter les conflits de noms entre classes
- [ ] C) A crypter le code source
- [ ] D) A creer des variables globales

---

### Question 3 - La fonction render()
Dans la fonction `render($path, $template = false, $data = [])`, que fait la fonction PHP `extract($data)` ?

- [ ] A) Elle supprime les donnees du tableau
- [ ] B) Elle transforme les cles du tableau en variables
- [x] C) Elle extrait uniquement les valeurs numeriques
- [ ] D) Elle compresse les donnees

---

### Question 4 - Le pattern MVC
Dans l'architecture MVC, quel est le role du Controleur ?

- [ ] A) Afficher les donnees a l'utilisateur
- [ ] B) Stocker les donnees en base de donnees
- [x] C) Gerer la logique metier et faire le lien entre Model et View
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

- [ ] A) A formater le HTML
- [x] B) A prevenir les attaques XSS (Cross-Site Scripting)
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

### Question 10 - La variable superglobale $_SERVER
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
- [ ] B) Pour crypter de maniere securisee et irreversible
- [ ] C) Pour valider la complexite du mot de passe
- [x] D) Pour generer des mots de passe aleatoires

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

- [ ] A) Le deuxieme parametre indique si on charge une 'views/' ou un 'templates/'
- [x] B) Le deuxieme parametre active ou desactive le cache
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

Les deux premières lignes servent à récupérer les données de utils.php et splAutoload.php
la variable $path prend comme valeur un URL
Dans le cas où il n'y aurai pas d'url donc seulement un slash, l'utilisateur est renvoyé vers indexController.php où il pourra se créer un compte, sinon l'url est découpé à chaque slash et $path est égal à la valeur d'index 1.
La variable $controllers prend comme valeur un chemin d'accés comptant $path.
Dans le cas où le chemin d'accès se trouvant dans $controllers existe, l'utilisateur est redirigé vers ce chemin, sinon une erreur 404 s'affiche.
_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

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
Les valeurs contenues dans $data sont importées, dans le cas où $data ne serai pas vide, l'utilisateur est renvoyé vers template/$path.php ($path contenant le nom d'un fichier) sinon l'utilisateur est renvoyé vers views/$path.php 

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

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
La variable $class contient une arborescence, le code permet de remplacer les reverse slash par des slash et de lancer par la suite le fichier php qui se trouverait au bout de cette arborescence
$class = \php-mvc-test\src\Models\User
 suite à ce code devient
$class= /php-mvc-test/src/Models/User.php
pour permettre une lecture dans un navigateur
_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

---

### Question 19 - Architecture et flux de donnees (1 point)

**Decrivez le chemin complet d'une requete HTTP dans cette application, depuis l'entree de l'utilisateur dans le navigateur jusqu'a l'affichage de la page. Mentionnez tous les fichiers traverses et leur role.**

Exemple : L'utilisateur tape `http://localhost/index` dans son navigateur...

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

---

### Question 20 - Securite et bonnes pratiques (1 point)

**Identifiez et expliquez 3 mesures de securite presentes dans ce projet (exemples : protection XSS, injection SQL, validation des donnees, etc.). Pour chaque mesure, citez le fichier et la ligne de code concernes.**

1. _______________________________________________________________________________

   _______________________________________________________________________________

2. _______________________________________________________________________________

   _______________________________________________________________________________

3. _______________________________________________________________________________

   _______________________________________________________________________________

---
