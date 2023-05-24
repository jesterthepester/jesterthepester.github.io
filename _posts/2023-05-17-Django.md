# Django How to Translation from Website

## Website

[Django 4.2 Documentation](https://docs.djangoproject.com/en/4.2/)

## Building A Django Project - Tutorial Part 1

### First Steps

First CD to do the directory

```Sh
cd /
django-admin startproject mysite
```

This script creates the below files and folders:

```Sh
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

These files are:

- The outer `mysite/` root directory is a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
- `manage.py`: A command-line utility that lets you interact with this Django project in various ways.
- The inner `mysite/` directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. `mysite.urls`).
- `mysite/__init__.py`: An empty file that tells Python that this directory should be considered a Python package.
- `mysite/settings.py`: Settings/configuration for this Django project.
- `mysite/urls.py`: The URL declarations for this Django project; a “table of contents” of your Django-powered site.
- `mysite/asgi.py`: An entry-point for ASGI-compatible web servers to serve your project.
- `mysite/wsgi.py`: An entry-point for WSGI-compatible web servers to serve your project.

### Starting The Server

First, you will meed to navigate to the (by default) `mysite/` location and then apply the migrations for the app.

```Sh
python manage.py migrate
```

Following this, we can run the server with the below script.

```Sh
python manage.py runserver
```

Following this, go to web browser and open `http://127.0.0.1:8000/`. By default the port is configured to 8000 but can be configured with the below script:

```Sh
python manage.py runserver 0.0.0.0:8080
```

### Creating Another App

Creating another app called `polls` in the `mysite` directory.

```Sh
python manage.py startapp polls
```

With the below structure:

```Sh
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

### Create a Url Script

Create a script called `urls.py` in the `polls` directory with the below code in it.

```Py
from django.urls import path
from . import views
urlpatterns = [
    path("", views.index, name="index"),
]
```

### Alter the Main Urls Script

In the `mysite/urls.py` script, import `include` package and add the polls path.

```Py
from django.contrib import admin
from django.urls import include, path
urlpatterns = [
    path("polls/", include("polls.urls")),
    path("admin/", admin.site.urls),
]
```

## Tutorial Part 2

### Database Link

The Django site can be deployed with various databases as outlined in the [documentation](https://docs.djangoproject.com/en/4.2/topics/install/#database-installation) such as oracle, mysql etc.

### Databases Settings

Change the engine and name below as per the database that has been deployed.

```Py
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": BASE_DIR / "db.sqlite3",
    }
}
```

### Managing Migrations

Running the below script migrates the polls `models.py` file into the current site.

```Sh
python manage.py makemigrations polls
```

### Managing the migrations to the DB

Running the below script will migrate the iteration `0001` into the database and commit the changes.

```Sh
python manage.py sqlmigrate polls 0001
```

### Check the Project Build

Script that checks the status of the project without migrating changes or touching the database.

```Sh
python manage.py check
```

### Managing the Shell

#### Starting the Shell

Starting the shell allows running of packages and other scripts.

```Sh
python manage.py shell
```

#### Example Script

```Sh
>>> from polls.models import Choice, Question
>>> Question.objects.all()
<QuerySet []>
# Create a new Question.
>>> from django.utils import timezone
>>> q = Question(question_text="What's new?", pub_date=timezone.now())
# Save the object into the database. You have to call save() explicitly.
>>> q.save()
# Now it has an ID.
>>> q.id
1
# Access model field values via Python attributes.
>>> q.question_text
"What's new?"
>>> q.pub_date
datetime.datetime(2012, 2, 26, 13, 0, 0, 775217, tzinfo=datetime.timezone.utc)
# Change values by changing the attributes, then calling save().
>>> q.question_text = "What's up?"
>>> q.save()
# objects.all() displays all the questions in the database.
>>> Question.objects.all()
<QuerySet [<Question: Question object (1)>]>
```

### Django Admin

#### Creating an Admin User

Creates administrator super user.

```Sh
python manage.py createsuperuserclass
```

### Start the Development Server

#### Script to Start

```Sh
python manage.py runserver
```

#### Log onto the Development Server

Log onto the server `http://127.0.0.1:8000/admin/` where you can manage your admin portal.

## Tutorial Part 3

### 

