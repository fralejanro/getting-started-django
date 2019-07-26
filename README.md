# Getting Started Django On Heroku

This repository was created to perform a rapid deployment of a django application on heroku, so the application only has the basic configurations for deploying on heroku.

## Content Structure 

These instructions will be divided into 4 parts, the first part is to clone this repository and make the deployment immediately in heroku, the second part is to explain what changes you must make if you want to continue with this application without changing the name of the project or the application, the third part is to explain what changes you must make if you want to change the name of the project and the application and the fourth part consists of a detailed guide of how the application was built until its deployment in heroku.

### Prerequisites

For the first part you must have Heroku Cli and Git installed, for the second and third part you must have Python, pip, Virtualenv and PostgreSQL installed, for the fourth part you must have everything installed.

* [Heroku Cli](https://devcenter.heroku.com/articles/heroku-cli#download-and-install) - Download and install Heroku Cli
* [Python](https://www.python.org/downloads/) - Download and install Python >= 3.7.3
* [pip](https://pip.pypa.io/en/stable/installing/) - Download and install pip >= 19.0.3
* [PostgreSQL](https://www.postgresql.org/download/) - Download and install PostgreSQL >= 10.9
* [Virtualenv](https://virtualenv.pypa.io/en/latest/installation/) - Download and install Virtualenv >= 16.4.3
* [Git](https://git-scm.com/downloads) - Download and install Git >= 2.17.1

## 1. Clone and deploy in heroku

As mentioned earlier this application was created to be deployed in heroku, so you only have to follow 5 steps to have your application running.

### Clone this repository

Clone this repository on your computer so you can work with it.

```
$ git clone https://github.com/alejandrodxf/getting-started-django.git mysite_project
```

### Log in heroku

Login to your heroku account

```
$ heroku login
```

### Create new app

Create a new app in heroku with a python buildpack

```
$ heroku create mysite --buildpack heroku/python
```

### Add a remote repository

Add a remote to your local repository using the name of your application

```
$ heroku git:remote -a mysite
```

### Deploying code

Use the ```git push``` command to push the code from your local repository’s master branch to your heroku remote

```
$ git push heroku master
```

## 2. Continue with this application without changing the name of the project or the application

If you want to continue experimenting with this application locally without changing the name of the project or application, just follow these 3 steps

### Clone this repository

Clone this repository on your computer so you can work with it.

```
$ git clone https://github.com/alejandrodxf/getting-started-django.git mysite_project
```

### Install the packages

To install the packages that are specified in the requirements.txt file you must perform 3 steps

#### Create a virtual environment
```
$ virtualenv env_mysite
```

#### Activate the virtual environment
```
$ source env_mysite/bin/activate
```

#### Install packages from requirements.txt
```
$ pip install -r requirements.txt
```

### Configure your database

Assuming that you are familiar with PostgreSQL and that you have already created databases before, change the NAME, USER and PASSWORD in the DATABASES section in the settings.py file for your data.

* The NAME refers to the name of your database
* The USER refers he username to use when connecting to the database
* The PASSWORD refers the password to use when connecting to the database

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

### Make your first migration

This application has not created models, however, to enter the django administrator it is necessary to perform a migration so that django by default creates the necessary tables for you to create your superuser.

#### Make the migrations
```
$ python manage.py migrate
```

#### Create the superuser
```
$ python manage.py createsuperuser
```

### Run the application

Finally run the application and verify that if you can enter the django administrator.

```
$ python manage.py runserver
```

## 3. Continue with this application changing the name of the project and the application

If you want to continue experimenting with this application locally without changing the name of the project or application, just follow these 3 steps and perform all the steps in part 2.

### Clone this repository

Clone this repository on your computer so you can work with it.

```
$ git clone https://github.com/alejandrodxf/getting-started-django.git mysite_project
```

### Change project name

Django does not provide a command to change the name of the project, so you will have to do it manually in several files and folders. The project in this repository is called 'mysite'.

#### Change the name of the mysite folder

Change the name of the mysite folder to the name you want your project to have. From now on you will have to continue using this same name to replace 'mysite'.

#### Change Procfile

Replace mysite in the next line of the Procfile file

```
web: gunicorn mysite.wsgi --log-file -
```
#### Change manage.py

Replace mysite in the next line of the manage.py file

```
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
```
#### Change wsgi.py

Replace mysite in the next line of the wsgi.py file

```
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
```

#### Change settings.py

Replace mysite in the following lines of the settings.py file

```
ROOT_URLCONF = 'mysite.urls'
WSGI_APPLICATION = 'mysite.wsgi.application'
```

### Change app name

Django does not provide a command to change the name of the app, so you will have to do it manually in several files and folders. The app in this repository is called 'myapp'.

#### Change the name of the myapp folder

Change the name of the myapp folder to the name you want your app to have. From now on you will have to continue using this same name to replace 'myapp'.

#### Change the name of the myapp folder inside templates folder

Chage the name the of the myapp folder that is inside templates

#### Change apps.py

Replace myapp in the following lines of the apps.py file

```
class MyappConfig(AppConfig):
    name = 'myapp'
```

#### Change views.py

Replace myapp in the next line of the views.py file

```
return render(request, 'myapp/home.html')
```

#### Change urls.py 

Replace myapp in the next line of the urls.py file

```
path('', include('myapp.urls')),
```

#### Change settings.py 

Replace myapp in the next line of the settings.py file

```
'myapp',
```
finally with the steps of part 2 skipping the repository cloning.

## 4. Create this repository from scratch

In this last part we will create this repository from scratch

#### Create a folder on your desktop to save all project files

```
~/Desktop$ mkdir mysite_project
```

#### Change to the folder you created earlier

```
~/Desktop$ cd mysite_project
```

#### Create a virtual environment for the project

```
~/Desktop/mysite_project$ virtualenv env_mysite
```

#### Activate the virtual environment

```
~/Desktop/mysite_project$ source env_mysite/bin/activate
```

#### Install django with pip

```
(env_mysite):~/Desktop/mysite_project$ pip install Django==2.2.3
```

#### Create a django project

```
(env_mysite):~/Desktop/mysite_project$ django-admin startproject mysite .
```

#### Create an application for the project

```
(env_mysite):~/Desktop/mysite_project$ django-admin startapp myapp
```

#### Change to project folder

```
(env_mysite):~/Desktop/mysite_project$ cd mysite
```

#### Add application 'myapp' in INSTALLED_APPS in the settings.py file

```
(env_mysite):~/Desktop/mysite_project/mysite$ nano settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
]

```

#### Install gunicorn, it's an http server

```
(env_mysite):~/Desktop/mysite_project/mysite$ pip install gunicorn
```

#### Install whitenoise, to serve static files

```
(env_mysite):~/Desktop/mysite_project/mysite$ pip install whitenoise
```

#### Add 'whitenoise.middleware.WhiteNoiseMiddleware', to the MIDDLEWARE in the settings.py file, it should be under 'django.middleware.security.SecurityMiddleware'

```
(env_mysite):~/Desktop/mysite_project/mysite$ nano settings.py
MIDDLEWARE = [
  # 'django.middleware.security.SecurityMiddleware',
  'whitenoise.middleware.WhiteNoiseMiddleware',
  ...
]
```
#### Install psycopg2-binary, is the PostgreSQL database adapter

```
(env_mysite):~/Desktop/mysite_project/mysite$ pip install psycopg2-binary
```

#### Configure the connection to the database

```
(env_mysite):~/Desktop/mysite_project/mysite$ nano settings.py

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

#### Install dj-database-url, this package allows you to use the environment variable DATABASE_URL

```
(env_mysite):~/Desktop/mysite_project/mysite$ pip install dj-database-url
```

#### Import dj_database_url and add the rest at the bottom of settings.py

```
(env_mysite):~/Desktop/mysite_project/mysite$ nano settings.py
import dj_database_url
.
.
.
db_from_env = dj_database_url.config(conn_max_age=500)
DATABASES['default'].update(db_from_env)
```

#### Install pillow, it is a library to work with images

```
(env_mysite):~/Desktop/mysite_project/mysite$ pip install pillow
```

#### Find yourself in the folder that contains all the project files and create the requirements.txt file that extracts the project requirements

```
(env_mysite):~/Desktop/mysite_project/mysite$ cd ..
(env_mysite):~/Desktop/mysite_project$ pip freeze > requirements.txt
```

#### Create the runtime.txt file and type the version of python you are using

```
(env_mysite):~/Desktop/mysite_project$ nano runtime.txt
python-3.7.3
```

#### Create the Procfile file and type

```
(env_mysite):~/Desktop/mysite_project$ nano Procfile
web: gunicorn mysite.wsgi --log-file -
```

#### Configure the path for static and multimedia files in settings.py

```
(env_mysite):~/Desktop/mysite_project$ cd mysite
(env_mysite):~/Desktop/mysite_project/mysite$ nano settings.py

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

#### Configure the url for static and multimedia files in urls.py

```
(env_mysite):~/Desktop/mysite_project/mysite$ nano urls.py

from django.conf import settings
from django.conf.urls.static import static
urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

#### Locate the folder that contains all the files in the application and create the folder for static files

```
(env_mysite):~/Desktop/mysite_project/mysite$ cd .. 
(env_mysite):~/Desktop/mysite_project$ cd myapp
(env_mysite):~/Desktop/mysite_project/myapp$ mkdir static
```

#### Locate the folder that contains all the files in the application and create the folder for static files

```
(env_mysite):~/Desktop/mysite_project/mysite$ cd .. 
(env_mysite):~/Desktop/mysite_project$ cd myapp
(env_mysite):~/Desktop/mysite_project/myapp$ mkdir static
```

#### Create the folder for the application templates

```
(env_mysite):~/Desktop/mysite_project/myapp$ mkdir templates
```

#### Go to the templates folder and create a folder with the name of the application

```
(env_mysite):~/Desktop/mysite_project/myapp$ cd templates
(env_mysite):~/Desktop/mysite_project/myapp/templates$ mkdir myapp
```

#### Create the template for the application home in the folder with the name of the application within templates

```
(env_mysite):~/Desktop/mysite_project/myapp/templates$ cd myapp
(env_mysite):~/Desktop/mysite_project/myapp/templates/myapp$ nano home.html
<h1>First deployment in heroku</h1>
```

#### Create a view for the home of the application in views.py

```
(env_mysite):~/Desktop/mysite_project/myapp/templates/myapp$ cd ..
(env_mysite):~/Desktop/mysite_project/myapp/templates$ cd ..
(env_mysite):~/Desktop/mysite_project/myapp$ nano views.py
def home (request):
	return render(request, 'myapp/home.html') 
```

#### Create the urls.py file and type a url for the home view

```
(env_mysite):~/Desktop/mysite_project/myapp$ nano urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'), 
]
```

#### Import include and create a url to get the application urls in project urls.py

```
(env_mysite):~/Desktop/mysite_project/myapp$ # cd ..
(env_mysite):~/Desktop/mysite_project$ cd mysite
(env_mysite):~/Desktop/mysite_project/mysite$ nano urls.py

from django.urls import include, path

urlpatterns = [
    path('', include('myapp.urls')),
]
```

#### Locate yourself in the folder that contains all the application files and create the forms.py file

```
(env_mysite):~/Desktop/mysite_project/mysite$ # cd ..
(env_mysite):~/Desktop/mysite_project$ cd myapp
(env_mysite):~/Desktop/mysite_project/myapp$ nano forms.py
```

#### Change in the settings.py file Debug = True and ALLOWED_HOSTS = []

```
(env_mysite):~/Desktop/mysite_project/myapp$ # cd ..
(env_mysite):~/Desktop/mysite_project$ cd mysite
(env_mysite):~/Desktop/mysite_project/mysite$ nano settings.py
DEBUG = False
ALLOWED_HOSTS = ['127.0.0.1', '.herokuapp.com']
```

#### Find a static folder and verify if you need to add new items

```
(env_mysite):~/Desktop/mysite_project/mysite$ # cd ..
(env_mysite):~/Desktop/mysite_project$ python3 manage.py collectstatic
```

#### Migrate the database

```
(env_mysite):~/Desktop/mysite_project$ python3 manage.py migrate
```

#### Create the .gitignore file and type

```
(env_mysite):~/Desktop/mysite_project$ nano .gitignore
 *.pyc
 *~
 env_mysite
 __pycache__
 /static
```

#### Create a git repository

```
(env_mysite):~/Desktop/mysite_project$ git init
```

#### Add all files to the preparation area

```
(env_mysite):~/Desktop/mysite_project$ git add .
```

#### Commit changes

```
(env_mysite):~/Desktop/mysite_project$ git commit -m "Init app"
```

Finally continue with all the steps of the first part skipping the repository cloning
