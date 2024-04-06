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
        ...,

        'DIRS': [os.path.join(BASE_DIR, 'Templates')],
        
        ...
    },
]
```

```
# Connect static files

STATIC_URL = 'static/'

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'Static')
]
```