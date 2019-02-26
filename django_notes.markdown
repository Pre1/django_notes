
# Terminal And settings.py 

## Setup the Virtual Environment

```bash
python3 -m venv <VIRTUAL_ENVIRONMENT_NAME>
```

##### Next, go into your virtual environment and activate it

```bash
source bin/activate
```

##### After activating the virtual environment we need to Install Django of clone an exist project

```bash
(virtualenv_name) pip install django
```

##### After we make sure tha the Django is installed, we can Create a Django project.

```bash
(virtualenv_name) django-admin startproject <PROJECT_NAME>
```

##### Go into the <PROJECT_NAME> directory and Create an App

```bash
(virtualenv_name) django-admin startapp <APP_NAME>
```

##### Run the server.

```bashbash
(virtualenv_name)$  ./manage.py runserver
```

##### Install the package to dealing with "Image Files"
```bash
(virtualenv_name)$ pip install pillow
```
##### To save all our packages that we've installed in the file requirements.txt, to make it easy to eny one to install it in one command

```bash
(virtualenv_name)$ pip freeze > requirements.txt
```

##### To see your Django packages in the terminal

```bash
(virtualenv_name)$ pip freeze
```

##### Or

```bash
(virtualenv_name)$ cat requirements.txt
```

##### Create a new migration for all our Models

```bash
(virtualenv_name)$ ./manage.py makemigrations
```

##### Confirm our migration

```bash
(virtualenv_name)$ ./manage.py migrate
```

##### To create super admin user in admin site that builted in Django

```bash
(virtualenv_name)$ ./manage.py createsuperuser
```

##### Using Django Shell in terminal

```bash
(virtualenv_name)$ ./manage.py shell
```

##### In Shell we write this command to view all Objects in any Model that we've created before

```bash
>>> ModelName.objects.all()
```
##### To retrieve a specific object of a model

```bash
>>> ModelName.objects.get(id=2)
```

##### To install "crispy-forms" package

```bash
(virtualenv_name)$ pip install django-crispy-forms
```

##### In settings file we have to add this line inside "INSTALLED_APPS list": 'crispy_forms',

##### And under "INSTALLED_APPS" we need to add this line

```python
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

##### After that we have to paste this line in the front of page that we'd like to use crispy form on it

```python
{% load crispy_forms_tags %}
```

##### Then we can use it by add it after the form word like this

```python
{{form|crispy}}
```

##### A package for authenticating using our social accounts

```bash
(virtualenv_name)$ pip install django-allauth
```

##### Install "requests" library that allows you to make requests to URLs and retrieve the responses, without any manual labor.

```bash
(virtualenv_name)$ pip install requests 
```

##### and we have to import it in the views file before we use it. This is an example how to use it.

```bash
import requests

url = 'https://api.github.com/events'
response = requests.get(url)
print(response.json())
```

##### Installing DRF "Django Rest Framework"

```bash
(virtualenv_name)$ pip install djangorestframework
(virtualenv_name)$ pip install markdown
(virtualenv_name)$ pip install django-filter
```

##### After that we have to add this line into "INSTALLED_APPS" in settings.py file *'rest_framework',*

##### To Remove the remote with Github
```bash
$ git remote rm origin 
```
##### To install django in server
```bash
(env_name_on_server) django@project_name_as_you_named:~$ apt-get install python3
```




---------------------------------------
---------------------------------------


# admin.py

##### To registering the models in admin file to show it up in the admin site, we shuld go to admin.py file and write the following lines

```python
from django.contrib import admin
from .models import ModelName

admin.site.register(ModelName)
```




---------------------------------------
---------------------------------------

# models.py

##### Import models from Django
```python
from django.db import models
```
##### Import the User's model from Django Framework
```python
from django.contrib.auth.models import User
```
##### This is how to create a new Model
```python
class ModellName(models.Model):
```

##### Example of the most useing field

```python

small_text = models.CharField(max_length=120)
big_text = models.TextField()
date_and_time = models.DateTimeField(auto_now_add=True)
just_time = models.TimeField(auto_now_add=True)
decimal = models.DecimalField(max_digits=10, decimal_places=3)
user = models.ForeignKey(User, default=1, on_delete=models.CASCADE) # To ManyToOne Relationship

class Meta:
	ordering = ['choose_field_01', 'choose_field_02']

def __str__(self):
    return self.small_text
```




---------------------------------------
---------------------------------------

# views.py

### Backages kinds


##### To import messages package
from django.contrib import messages

##### To import the Q package that dealing with the search
```python
from django.db.models import Q

# And use it like this
query = request.GET.get("name_of_html_form_tag")
	if query:
		restaurants = restaurants.filter(
			Q(Field1__icontains = query)|
			Q(Field2__Field1OfField2__icontains = query)|
			Q(Field3__icontains = query)
		).distinct()
```
##### If we'd like to returning an HttpResponse, which returns a string to the webpage we've to import "HttpResponse" like so
```python
from django.http import HttpResponse
```

##### Import 404 page from django
```python
from django.http import Http404
```

##### Import Json Response
```python
from django.http import JsonResponse
```

##### And use it like this
```python
def function_name(request):
    return HttpResponse("<h1> Hello Ayman </h1>")
```

##### If we'd like to send our data to some template's files we have to import "render" and import "redirect" to using url's name in the views.py like this
```python
from django.shortcuts import render, redirect
```

##### And use it like this
```python
context = {
	"whatever": whatever_object,
	}
return render(request, 'page.html', context)
```

---------------------------------------
---------------------------------------


##### import django permission
```python
from rest_framework.permissions import AllowAny, IsAuthenticated, IsAdminUser
```
##### Import it to help us using "rest_framework"

```python
from rest_framework.generics import ListAPIView, RetrieveAPIView, CreateAPIView, RetrieveUpdateAPIView, DestroyAPIView
```

```python
# Import forms.py and it's classes
from .forms import ModelNameForm

# Import serializers.py and it's classes
from .serializers import ModelNameSerializer
```

```python
# And use it like this for "object_list"
class ListView(ListAPIView):
    queryset = ModelName.objects.all()
    serializer_class = ListSerializer

# And use it like this for "object_detail"
class DetailView(RetrieveAPIView):
    queryset = ModelName.objects.all()
    serializer_class = DetailSerializer
    lookup_field = 'id'
    lookup_url_kwarg = 'object_id'

class CreateView(CreateAPIView):
    serializer_class = CreateSerializer

    def perform_create(self, serializer):
        serializer.save(author=self.request.user)

class UpdateView(RetrieveUpdateAPIView):
    queryset = ModelName.objects.all()
    serializer_class = UpdateSerializer
    lookup_field = 'id'
    lookup_url_kwarg = 'object_id'

class DeleteView(DestroyAPIView):
    queryset = ModelName.objects.all()
    serializer_class = DestroyAPIView
    lookup_field = 'id'
    lookup_url_kwarg = 'object_id'

    # How to use permission
    permission_classes = [IsAuthenticated, IsAdminUser]

```

---------------------------------------
---------------------------------------
# urls.py
### Backages kinds

```python

# To use admin site
from django.contrib import admin 

# To use path package
from django.urls import path

# To access to views's Functions
from <APP_NAME> import views

# To access to views's Classes
from <APP_NAME>.views import <CLASS_NAME>

# Static and Media Files Setup ###
from django.conf import settings
from django.conf.urls.static import static
```

### path kinds "Inside urlpatterns list"

##### Path to accessing the views file's functions. we use it usual with the full stack applications

```python
path('whatever/', views.FUNCTION_NAME, name='url_name'),
```

##### Path to accessing the views file's classes. we use it usually with the APIs:

```python
path('whatever/', CLASS_NAME.as_view(), name='url_name'),
```

# Passing data through the url
path('whatever/whatever/<int:object_id>/', views.FUNCTION_NAME, name='url_name'),


# --- "Under urlpatterns list" --- #

### Static and Media Files Setup ###

# Static Setup

urlpatterns+=static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)

# Media Setup

urlpatterns+=static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)


---------------------------------------
---------------------------------------

# settings.py 
# Static Files Setup 

```python
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

### Media Files Setup ###

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```



---------------------------------------
---------------------------------------


# forms.py 

##### Import forms from Django
```python
from django import forms
```
##### Import models we've created
```python
from .models import ModelName, ModelName
```

##### This is how to create a new Model Form

```python
class ModelNameForm(forms.ModelForm):
    class Meta:
        model = ModelName
        fields=['field_1', 'field_2', 'field_3']

```


---------------------------------------
---------------------------------------

### serializers.py ###

##### A serializer allows us to work with data in a very specific way. It turns our data into JSON and also does validation. You'll come to see that serializers work in a very similar way to forms.

##### We have to import the package first

```python
from rest_framework import serializers
from .models import ModelName

class ListSerializer(serializers.ModelSerializer):
    class Meta:
        model = ModelName
        fields = ['field_1', 'field_2', 'field_3',]
```


---------------------------------------
---------------------------------------

### permissions.py ###



    
