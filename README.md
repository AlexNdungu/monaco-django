# Django And Monaco Code editor

**Django** is a high-level Python web framework that simplifies the process of creating web applications using Python.

**The Monaco Editor** is the fully featured code editor from **Microsoft**.

## Set Up

### 1. Create and Configure A Django Project

```
$ django-admin startproject project_name

$ python manage.py startapp app_name
```

### 2. Django - settings.py

```
import os

# Add app to installed apps

INSTALLED_APPS = [
    ...,

    'app_name',
]

```

```
# Connect Templates

TEMPLATES = [
    {
        ...

        'DIRS': [os.path.join(BASE_DIR, 'Templates')],
        
        ...
    },
]
```

```
# Connect static files

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'Static')
]
```


### 3. Django - views.py

```
from django.shortcuts import render

# Create your views here.

def index(request):
    return render(request, 'index.html')
```

### 4. Django - urls.py

```
# urls in main folder

from django.contrib import admin
from django.urls import path, include
from django.conf.urls.static import static
from django.conf import settings

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('editor.urls')),
]

# Connect staticfile path to main url

urlpatterns += static(settings.STATIC_URL, document_root = settings.STATIC_ROOT)
```

```
# urls in the app folder

from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```
### 5. Django - Templates - index.html

- Create a html file in the Templates folder

```
{% load static %}
<head>

    <link rel="stylesheet" href="{% static 'index.css' %}">

    <!--This line links the html file with the monaco editor css file-->
    <link
			rel="stylesheet"
			data-name="vs/editor/editor.main"
			href="{% static 'node_modules/monaco-editor/min/vs/editor/editor.main.css' %}"
	/>

    <!--These lines links the editor’s source scripts to the template-->

    <script src="{% static 'node_modules/monaco-editor/min/vs/loader.js' %}"></script>
    <script src="{% static 'node_modules/monaco-editor/min/vs/editor/editor.main.nls.js' %}"></script>
    <script src="{% static 'node_modules/monaco-editor/min/vs/editor/editor.main.js' %}"></script>

</head>
<body>

    <div id="the_editor">
    </div>
    
    <script>

        // This js code initializes the monaco editor onto the domElement > the_editor

        var editor = monaco.editor.create(document.getElementById('the_editor'), {
            value: ['function x() {', '\tconsole.log("Hello world!");', '}'].join('\n'),
            language: 'javascript',
        });
    </script>
    
</body>
```

### 6. Monaco Editor - npm install

- You will have to open the **Static directory** in your terminal to install the Monaco package.

```
$ npm install monaco-editor
```

- Afterwards, add **.gitignore** code if you intend to use git and github.

```
app_name/migrations/0*
app_name/migrations/__pycache__/*
app_name/__pycache__/*
project_name/__pycache__/*

Static/package-lock.json
Static/package.json
Static/node_modules/.package-lock.json
Static/node_modules/monaco-editor/dev
Static/node_modules/monaco-editor/esm
Static/node_modules/monaco-editor/CHANGELOG.md
Static/node_modules/monaco-editor/LICENSE
Static/node_modules/monaco-editor/monaco.d.ts
Static/node_modules/monaco-editor/package.json
Static/node_modules/monaco-editor/README.md
Static/node_modules/monaco-editor/ThirdPartyNotices.txt
staticfiles

``