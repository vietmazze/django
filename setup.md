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
   - `from django.urls import path
   - from . import views
   - urlpatterns = [path('', views.index, name='index'),]`
   
