# Symfony - Doctrine -PHP

## Sommaire
* Installation
* Créer environnement de travail et projet
* Lancer eclipse
* Ouvrir localhost
* Créer BDD
  * Config
  * Créer entité
  * Créer bdd
  * Persistence
  * Verification
  * Utilisateur
* Fixtures
* Commandes
  * But
  * Exemple
  * Créer
  * Vérifier
  * TIPS
* Controller
  * Créer
* CRUD (génère entity, controleur, formulaires, templates)
* Formulaires
* Session
* Routage
* Gabarit TWIG
* Bootstrap
  * Configuration
  * Menus
* Upload images
* Form dynamique AJAX
* Source

## Installation

Pour débuter il faut php, composer, XML, SQLite3

Pour verifier:

```
composer -V
php -v 
php -m | grep xml
php -m | grep sqlite //Pour voir sqlite3
```
Sinon:

https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx
```
sudo apt install php-xml/php sqlite3
```

## Créer environnement de travail et projet

```
mkdir $HOME/Dev/ProjetPHP/mon-projet
cd $HOME/Dev/ProjetPHP/mon-projet
composer create-project -s stable symfony/skeleton monprojet ~4
ls monprojet //->bin  composer.json  composer.lock  config  public  src  symfony.lock  var  vendor
cd monprojet
composer update
bin/console -V //version symfony
```

## Lancer eclipse ouvrir localhost

On va utiliser la bibliothèque PHP Doctrine, qui est un ORM (Object Relational Mapper). Son rôle est de permettre la gestion de collections d’objets, d’associations entre entités, et de fournir le chargement/sauvegarde des objets depuis la base de données.

```
/opt/eclipse/CSC4101/php-2019-06/eclipse/eclipse
```

Créer nouveau workplace ds $HOME/Dev/ProjetPHP/.

ProjectExplorer/Import projects/PHP/Symfony project/Next et utiliser mon-projet.

Project/Proprierties/Project natures on doit avoir Symfony Project Nature et Doctrine Project Nature sinon ajouter.

Configuration test: 
* File/Open/monprojet 
* afficher fichierscachés  
* .env 
* DATABASE_URL=sqlite:///%kernel.project_dir%/var/data.db

**TIPS**
Refresh ou recharger régulièrement. Nettoyer le cache.

## Ouvrir localhost
```
php -S "[::0]":8000 -t public
```

Ou
```
composer require symfony/web-server-bundle --dev //Installer
composer require profiler --dev  //Installer
bin/console cache:clear

bin/console server:run  //ouvrir http://127.0.0.1:8000
```

## Créer BDD

**Configuration / Installation**
```
composer require symfony/orm-pack //doctrine accès bdd via object php
composer require --dev symfony/maker-bundle //make bundle génère code php
composer require --dev doctrine/doctrine-fixtures-bundle //dataFixtures charger données test dans bdd
```

**Créer entité**
```
php bin/console make:entity
```

Après suivre guide. A du créer src/Entity/Nom.php et src/Repository/NomRepository.php

Pour du OneToMany etc créer première sans et ensuite seconde préciser.

**Créer bdd**
```
php bin/console doctrine:database:drop --force
php bin/console doctrine:database:create //fichier
php bin/console doctrine:schema:create //schema
```

**Persistence**

Ds OnToMany->
```
/**
 * @ORM\OneToMany(targetEntity="App\Entity\Recommendation", mappedBy="film", orphanRemoval=true, cascade={"persist"})
 */
private $recommendations;
```

**Verification**

```
php bin/console doctrine:query:sql 'SELECT * FROM film'
```

## Fixtures

```
php bin/console doctrine:fixtures:load -n
```

## Commandes
**But**

Créer facilement requete SQL en cas de bugs

**Exemple**
```
// ...

use App\Entity\Film;
use App\Repository\FilmRepository;
use Symfony\Component\DependencyInjection\ContainerInterface;

// ...

class ListFilmsCommand extends Command
{
    /**
     * @var FilmRepository
     */
    private $filmRepository;

    public function __construct(ContainerInterface $container)
    {
    parent::__construct();
    $this->filmRepository = $container->get('doctrine')->getManager()->getRepository(Film::class);
    }

    //...


protected function execute(InputInterface $input, OutputInterface $output)
    {
        $films = $this->filmRepository->findAll();
        if(!$films) {
        $output->writeln('<comment>no films found<comment>');
        exit(1);
        }

        foreach($films as $film)
        {
        $output->writeln($film);
        }

    }
```

**Créer**
```
bin/console make:command //Exemple name: app:list-films -> crée src/Command/ListFilmsCommand.php
```

**Vérifier **
```
bin/console list app
bin/console app:list-films --help
bin/console app:list-films
```

**Utilisateur**

```
bin/console make:user
bin/console  make:migration
php bin/console doctrine:migrations:migrate
bin/console make:auth
bin/console cache:clear
```

A voir:

[How to Build a Login Form](https://symfony.com/doc/4.4/security/form_login_setup.html)
[ Finishing the login form ](https://symfony.com/doc/4.4/security/form_login_setup.html#finishing-the-login-form)

Enlever com ds src/Security/LoginFormAuthenticator.php si login
 
logout:
 ```
security:
   ...
   firewalls:
        ...
        main:
            logout:
                path: app_logout
                # where to redirect after logout
                target: app_any_route
```

Hierachie:
```
security:
    ...
    role_hierarchy:
	ROLE_ADMIN:       ROLE_USER
	ROLE_SUPER_ADMIN: ROLE_ADMIN
```

Donc menus différents:
```
bootstrap_menu:
  menus:
    main:
...
    anonymousaccount:
      items:
        account:
          label: 'Account'
          items:
            login:
              label: 'Login'
              route: 'app_login'
#            register:
#              label: 'Register'
#              route: 'app_register'
    account:
      items:
        account:
          label: 'Account'
          items:
            logout:
              label: 'Logout'
              route: 'app_logout'
              roles: [ 'ROLE_USER' ]
```
```
<div class="collapse navbar-collapse" id="navbarResponsive">
     <ul class="navbar-nav ml-auto">
             {{ render_bootstrap_menu('main') }}
     </ul>
</div>
{% if app.user %}
<div class="collapse navbar-collapse" id="navbarsAccountDefault">
     <ul class="navbar-nav ml-auto">
             {{ render_bootstrap_menu('account') }}
     </ul>
</div>
{% else %}
<div class="collapse navbar-collapse" id="navbarsAnonAccountDefault">
     <ul class="navbar-nav ml-auto">
             {{ render_bootstrap_menu('anonymousaccount') }}
     </ul>
</div>
{% endif %}
```

Gestion accès
```
{% if is_granted('ROLE_USER') %}
    <a href="{{ path('todo_edit', {'id': todo.id}) }}">edit</a>
{% endif %}
```
```
use Sensio\Bundle\FrameworkExtraBundle\Configuration\IsGranted;
...
    /**
     * @Route("/{id}/edit", name="todo_edit", methods={"GET","POST"})
     * @IsGranted("ROLE_USER")
     */
    public function edit(Request $request, Todo $todo): Response
 ```
 ```
 if ($todo->getCompleted() == false) {
    $this->denyAccessUnlessGranted('ROLE_ADMIN');
}
```

**TIPS**
```
public function __toString() {
    return $this->title . " (" . $this->year . ")";
}
```

## Controller

**Créer**
```
bin/console make:controller NomController
```

## CRUD (génère entity, controleur, formulaires, templates)
```
bin/console make:entity //Puis rafraichir
bin/console make:migration
bin/console doctrine:migrations:migrate
bin/console make:crud //Même nom qu'à make:entity puis rafraichir
bin/console cache:clear
```
Attention templates/entity/truc surchage body changer si besoin main par exemple

## Formulaires
Utilisation bootstrap ans config/packages/twig.yaml
```
twig:
    ...
    form_themes: ['bootstrap_4_layout.html.twig']
```
Dans template *Attention inclure différent de surcharger*
```
{{ include('paste/_form.html.twig') }}
```

## Session
```
$urgents = array();
$urgents = $this->get('session')->get('urgents');
if( ! is_array($urgents) ) {
   ...
}
$this->get('session')->set('urgents', $urgents)
```

```
{% set urgents = app.session.get('urgents') %}
{% dump(urgents) %}
{% if todo.id in urgents %}
URGENT
{% else %}
NOT URGENT
{% endif %}
```
## Routage

Accès table de routage
```
bin/console debug:router
```

Si nouvelle route fonctionne pas
```
bin/console debug:router
```

Si tjr pas
```
rm -fr var composer.lock symfony.lock vendor
php -d memory_limit=-1 /usr/bin/composer install
```

## Gabarit Twig

Dans répertoire template : index.html.twig
```
{% extends 'base.html.twig' %}

{% block title %}Welcome!{% endblock %}

{% block body %}
<h1>Welcome</h1>

    <p>{{ welcome }}</p>

{% endblock %} {# body #}



/**
 * @Route("/", name = "home", methods="GET")
 */
public function indexAction()
{
    return $this->render('index.html.twig',
        [ 'welcome' => "Bonne utilisation de la todo list" ]
    );
}
```

base.html.twig
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Welcome!</title>
    </head>
    
    <body>
        <h1>Welcome</h1>
    </body>
</html>
```

## Bootstrap

**Configuration**

Position ds projet Symfony de l'app. Dans public extraire la distrib de [Start Bootstrap](https://startbootstrap.com/)
```
 wget https://github.com/StartBootstrap/startbootstrap-bare/archive/gh-pages.zip
unzip gh-pages.zip
```

Dans head page html:
```
<link href="vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet">
<link href="{{ asset('vendor/bootstrap/css/bootstrap.min.css') }}" rel="stylesheet"> //mieux avec asset car qu'une modif à faire
```
Avant fin body page html
```
  <script src="vendor/jquery/jquery.slim.min.js"></script>
  <script src="vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
```
Dans config/packages/framework.yaml
```
framework:
  ...
    assets:
	base_path: '/startbootstrap-bare-gh-pages'
```
*Attention si erreur avec asset*
```
php -d memory_limit=-1 /usr/bin/composer require symfony/asset
```

Exemple modif templates/bases.html.twig
```
{% block body %}
  <div class="container body-container">
    <main>
      {% block main %}
      <div class="row">
        <div class="col-md-12">
          <p>
            <i>MAIN</i>
          </p>
        </div>
      </div>
      {% endblock %} {# main #}
    </main>
  </div> <!-- /.body-container -->
  {% block footer %}
  <div class="row">
    <div class="col-md-12">
      <footer>
        <p>FOOTER</p>
      </footer>
    </div>
  </div>
  {% endblock %}{# footer #}
{% endblock %} {# body #}
```

**Menu*

Installation
```
php -d memory_limit=-1 /usr/bin/composer require camurphy/bootstrap-menu-bundle
```

Créer onfig/packages/boostrap_menu.yaml
```
bootstrap_menu:
  menus:
    main: //nom menus à appeler
      items:
        todos:
          label: 'Tasks'
          route: 'todo_list'

```
Dans templates/base.html.twig
```
 {% block menu %}
  <!-- Navigation -->
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark static-top">
    <div class="container">
      <a class="navbar-brand" href="#">Todo App</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarResponsive">
        <ul class="navbar-nav ml-auto">
          {{ render_bootstrap_menu('main') }}
        </ul>
      </div>
    </div>
  </nav>
  {% endblock %}{# menu #}

```

## Upload images

Dispo cours
 
## Form dynamique AJAX
 
Dispo cours
 
## Source

Cours: Architectures et applications web

Mots-clés: Web, MVC, HTML, CSS, JavaScript, AJAX, DOM, PHP, HTTP, Symfony, ReST
