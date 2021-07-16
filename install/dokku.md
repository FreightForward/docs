---
layout: default
title:  Deploy - DOKKU Container
parent: Installation
nav_order: 2
has_children: false
---

`dj-database-url` is a dsn parser. You can ignore it if you do not use dsn notation for database connection.

#### settings.py

Rewrite the database connection fragment.
<br>e.g., Instead of
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('FREIGHTAPP_DB_NAME'),
        'USER': os.environ.get('FREIGHTAPP_DB_USER'),
        'PASSWORD': os.environ.get('FREIGHTAPP_DB_PASS'),
        'HOST': os.environ.get('FREIGHTAPP_DB_HOST'),
        'PORT': os.environ.get('FREIGHTAPP_DB_PORT'),
    }
}
```

Replace that fragment with this:
```python
DATABASES = {
    'default': dj_database_url.config()
}
```
