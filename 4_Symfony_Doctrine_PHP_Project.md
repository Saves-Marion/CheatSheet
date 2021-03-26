# Symfony - Doctrine -PHP

## Sommaire
* Installation
* Créer environnement de travail et projet
* Lancer eclipse
* Créer BDD
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

## Lancer eclipse

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

## Créer BDD

Configuration / Installation
```
composer require symfony/orm-pack //doctrine accès bdd via object php
composer require --dev symfony/maker-bundle //make bundle génère code php
composer require --dev doctrine/doctrine-fixtures-bundle //dataFixtures charger données test dans bdd
```
Créer entité
```
php bin/console make:entity
```
Après suivre guide. A du créer src/Entity/Nom.php et src/Repository/NomRepository.php

Pour du OneToMany etc créer première sans et ensuite seconde préciser.

Créer bdd
```
php bin/console doctrine:database:drop --force
php bin/console doctrine:database:create //fichier
php bin/console doctrine:schema:create //schema
```

## Source

Cours: Architectures et applications web

Mots-clés: Web, MVC, HTML, CSS, JavaScript, AJAX, DOM, PHP, HTTP, Symfony, ReST
