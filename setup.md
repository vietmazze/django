# DJANGO SETUP

### Basics commandline
1. `django-admin startproject mysite`
    - The outer mysite/ root directory is just a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
    - manage.py: A command-line utility that lets you interact with this Django project in various ways. You can read all the details about manage.py in django-admin and manage.py. 
    - The inner mysite/ directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. mysite.urls).
    - mysite/__init__.py: An empty file that tells Python that this directory should be considered a Python package. 
            - This allow us to import submodule by letting Python knows the folder with _init_ contains packages.
    - mysite/settings.py: Settings/configuration for this Django project. Django settings will tell you all about how settings work.
    - mysite/urls.py: The URL declarations for this Django project; a “table of contents” of your Django-powered site. You can read more about URLs in URL dispatcher.
    - mysite/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project. See How to deploy with WSGI for more details.
2. ` python manage.py runserver` 
    - This will satart up the development server
3. `python manage.py startapp polls`
    - Creates an app folder `polls` 

### Files inside an app 
1. polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
    
2. polls/views.py : What the website will show 
   - from django.http import HttpResponse
   - def index(request):
   - return HttpResponse("Hello, world. You're at the polls index.")
3. In order to link views,  we need to map it to a URL - and for this we need a URLconf.   
   - create a new urls.py
   - `from django.urls import path`
   - `from . import views`
   - `urlpatterns = [path('', views.index, name='index'),]`
4. Also need to point link to root URLs, mysite/urls.py
    - urlpatterns = [
    - path('polls/', include('polls.urls')),
    - path('admin/', admin.site.urls),]


### Setting up Database/ Admin
1. Database setup in mysite/settings.py, we must include the database we wanted to work in this case Postresql. 
    - Set up database through Postsql `createdb [OPTION][NAME]` and install connector psycopg2 
    - Make sure to add in username/host/ etc on settings.py so they are connected
    - `DATABASES = {`
    -  `'default': {`
    -   ` 'ENGINE': 'django.db.backends.postgresql_psycopg2',`
    -   ` 'NAME': 'poll_django',`
    -   ` 'USER': 'postgres',`
    -   ` 'PASSWORD': 'HIGHpoint-123',`
    -    `'HOST':'localhost',`
    -   ` 'PORT':'',`
2. Migrate data: `python manage.py migrate` 
    - Need to create database tables by migration
3. Creating models: Essentially a database layout, what columns, rows etc.. will be in your database.
    - from django.db import models
    - class Question(models.Model):
    - question_text = models.CharField(max_length=200)
    - pub_date = models.DateTimeField('date published')
 4. Activating Models
    - Go in mysite/settings.py and add in the class created by polls/apps.py 
    - INSTALLED_APPS =
    - 'polls.apps.PollsConfig',
    - 'django.contrib.admin',
 5. Cont Activation
    - python manage.py makemigrations polls ( Tell django you have made changes to models)
    -  python manage.py sqlmigrate polls 0001 ( To check your database as you wanted in SQL)
    - python manage.py migrate ( Do it again to create the models changes to database)
 6. Playing with the API
    - python manage.py shell
    - From here you can play around with the database you created
```>>> from polls.models import Choice, Question  # Import the model classes we just wrote.

# No questions are in the system yet.
>>> Question.objects.all()
<QuerySet []>

# Create a new Question.
# Support for time zones is enabled in the default settings file, so
# Django expects a datetime with tzinfo for pub_date. Use timezone.now()
# instead of datetime.datetime.now() and it will do the right thing.
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
datetime.datetime(2012, 2, 26, 13, 0, 0, 775217, tzinfo=<UTC>)

# Change values by changing the attributes, then calling save().
>>> q.question_text = "What's up?"
>>> q.save()

# objects.all() displays all the questions in the database.
>>> Question.objects.all()
<QuerySet [<Question: Question object (1)>]> 
```

7. Creating an admin user
    - python manage.py createsuperuser
    -Start the server and go in admin section http://127.0.0.1:8000/admin/
    
### Templates: 
1. Templates is use with views to show the html side of django.
 
```{% extends "base.html" %}
{% block title %}Index{% endblock %}
{% block head %}
    {{ super() }}
    <style type="text/css">
        .important { color: #336699; }
    </style>
{% endblock %}
{% block content %}
    <h1>Index</h1>
    <p class="important">
      Welcome to my awesome homepage.
    </p>
{% endblock %}
```

    - {% ... %} for Statements like for loop
    - {{ ... }} for Expressions like str, tuples
    - The href attribute specifies the link's destination: <a href="https://www.w3schools.com">Visit W3Schools</a>
   
