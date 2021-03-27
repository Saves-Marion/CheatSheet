# Django - Python 

## Sommaire
* Installation Configuration
* Créer projet
* Créer une base de données
* Créer application
* Autres

## Installation Configuration
Pour Django
```
mkdir mon-projet
cd mon-projet
virtualenv env -p python3
. env/bin/activate
pip install django
python -m django --version
```
Pour PostgreSQL

A voir / installer:
* [PostgreSQL](https://www.postgresql.org/download/)
* [pgAdmin pour visualiser autre ligne commande](https://www.pgadmin.org/download/)

```
pip install psycopg2
psql //verif
postgres -D /usr/local/pgsql/data //demarrer serveur
```

## Créer projet
```
django-admin startprojet monprojet

./manage.py runserver //localhost:8000
```

## Créer une base de données
```
$ createdb -O username dbname
psql //voir les bdd puis \l ou \h
```
Puis l'ajouter à Django
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql', # on utilise l'adaptateur postgresql
        'NAME': 'dbname', 
        'USER': 'username', 
        'PASSWORD': '',
        'HOST': '',
        'PORT': '5432',
    }
}


./manage.py migrate
```

## Créer application

> C'est un ensemble de fonctionnalité liées entre elles et cohérente.

Ne pas hésiter à en faire une partie partie du projet. Si externe voir les pages d'installation potentiel settings ou url à modifier.

```
$ django-admin startapp store //store = nom ici

INSTALLED_APPS = [
    'store.apps.StoreConfig',
    # ...
]
```

**Toolbar**
[Debug Toolbar](https://github.com/jazzband/django-debug-toolbar)
```
pip install django-debug-toolbar

INSTALLED_APPS = [
    # ...
    'django.contrib.staticfiles',
    'debug_toolbar',
]
```

## Autres

On a deja **models.py** et **views.py**

Dans les applications repertoire **templates** et sous-rep **nomappli**

Créer fichiers dans les appli **urls.py** dans projet/urls.py importer
```
urlpatterns = [
    url(r'^appli/', include('appli.urls')),
    url(r'^admin/', admin.site.urls)
]
```
