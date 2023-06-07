---
title: "Starting a project in Django"
datePublished: Wed Jun 07 2023 08:08:33 GMT+0000 (Coordinated Universal Time)
cuid: clilfh6pd001b09ky500h2h4h
slug: starting-a-project-in-django

---

1. Install all the setup and requirements to start a Python project.
    

```python
python3 -m pip install django 
```

1. After installing Django and pip, Please refer to the instalment of the Django and pip in the attached document.
    

[https://docs.djangoproject.com/en/4.2/topics/install/](https://docs.djangoproject.com/en/4.2/topics/install/)

Now starting a project in Django:

1. Run the code: django-admin startproject CRM
    
2. After that run the command: : django-admin startapp Website
    
3. After that your vs code will look similar like this:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686124488187/191ecc36-1e66-4c72-a683-d619805dad3e.png align="center")

1. After that setup then create the urls.py file in your app file. In this scenario Website is the app and CRM is the project.
    
2. Lets setup our urls files: CRM URLS
    

```python
from django.contrib import admin
from django.urls import path , include 

urlpatterns = [
    path('admin/', admin.site.urls),
    path ('', include('Website.urls')),
]
```

1. After that setup the urls file of our APP: Website as shown below:
    

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name = 'home'),
    
]
```

1. After this setup, dont forgot to register your app in the setting.py file in Project.
    

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'Website',
   
]
```

1. After this setup your views so that it can render the file.
    

```python
from django.shortcuts import render

# Create your views here.


def home(request):
    return render(request, 'home.html', {})
```

1. For that create new folder templates and create home.html in that folder in the app. In this scenerio Website as shown below:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686125194826/e0a0a428-af97-44b9-b84e-b11472673887.png align="center")

1. After that it will render your file while loading. For that run python3 manage.py runserver. You can run this command before all this steps.
    
    to create a superuser you can run the command: python3 manage.py createsuperuser