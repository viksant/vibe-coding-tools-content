---
title: "Enhanced Cursor Django REST Framework Configuration"
description: "Comprehensive setup for Django REST API development with DRF, PostgreSQL, and Celery integration."
category: "configuration"
tags: ["cursor", "django", "rest-framework", "api", "postgresql", "python", "celery", "redis"]
tech_stack: ["python", "django", "drf", "postgresql", "redis", "celery"]
---

This configuration sets you up for developing a Django REST API with DRF, PostgreSQL, and Celery.

### Configuration Overview
With this setup, you can create powerful RESTful APIs using the Django REST Framework (DRF), PostgreSQL as your database, and Celery for handling background tasks.

### Prerequisites
Before you dive in, make sure you have the following installed:
- Python 3.8 or a newer version
- Django 3.2 or later
- Django REST Framework 3.12 or higher
- PostgreSQL 12 or above
- Redis (needed for Celery)
- pip (Python's package installer)

### Installation & Setup
Let's walk through the steps to get everything running:

1. **Create a new Django project**:
   ```bash
   django-admin startproject myproject
   cd myproject
   ```

2. **Install the required packages**:
   ```bash
   pip install django djangorestframework psycopg2-binary celery redis
   ```

3. **Create a new Django app**:
   ```bash
   python manage.py startapp myapp
   ```

4. **Update `settings.py` to include your app and DRF**:
   ```python
   INSTALLED_APPS = [
       ...
       'rest_framework',
       'myapp',
   ]
   ```

5. **Set up your PostgreSQL database in `settings.py`**:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': 'mydatabase',
           'USER': 'myuser',
           'PASSWORD': 'mypassword',
           'HOST': 'localhost',
           'PORT': '5432',
       }
   }
   ```

6. **Set up Celery in `myproject/celery.py`**:
   ```python
   from __future__ import absolute_import, unicode_literals
   import os
   from celery import Celery

   os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')
   app = Celery('myproject')
   app.config_from_object('django.conf:settings', namespace='CELERY')
   app.autodiscover_tasks()
   ```

7. **Add Celery configuration in `settings.py`**:
   ```python
   CELERY_BROKER_URL = 'redis://localhost:6379/0'
   ```

8. **Create a sample model in `myapp/models.py`**:
   ```python
   from django.db import models

   class Item(models.Model):
       name = models.CharField(max_length=100)
       description = models.TextField()
   ```

9. **Set up a serializer in `myapp/serializers.py`**:
   ```python
   from rest_framework import serializers
   from .models import Item

   class ItemSerializer(serializers.ModelSerializer):
       class Meta:
           model = Item
           fields = '__all__'
   ```

10. **Create API views in `myapp/views.py`**:
    ```python
    from rest_framework import viewsets
    from .models import Item
    from .serializers import ItemSerializer

    class ItemViewSet(viewsets.ModelViewSet):
        queryset = Item.objects.all()
        serializer_class = ItemSerializer
    ```

11. **Configure URLs in `myapp/urls.py`**:
    ```python
    from django.urls import path, include
    from rest_framework.routers import DefaultRouter
    from .views import ItemViewSet

    router = DefaultRouter()
    router.register(r'items', ItemViewSet)

    urlpatterns = [
        path('', include(router.urls)),
    ]
    ```

12. **Include your app's URLs in `myproject/urls.py`**:
    ```python
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('api/', include('myapp.urls')),
    ]
    ```

13. **Run the migrations**:
    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```

14. **Start the Django server**:
    ```bash
    python manage.py runserver
    ```

15. **Launch the Celery worker**:
    ```bash
    celery -A myproject worker --loglevel=info
    ```

### File Structure
Here’s a quick look at what your project should look like:
```
myproject/
│
├── myproject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── celery.py
│
├── myapp/
│   ├── migrations/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   └── views.py
│
└── manage.py
```

### Key Configuration Files
- **`settings.py`**: This file holds your database and Celery settings.
- **`celery.py`**: This file initializes Celery with your Django settings.
- **`models.py`**: Here, you define your database models.
- **`serializers.py`**: This file maps your models to JSON format.
- **`views.py`**: This file implements your API logic.

### Advanced Options
Want to take it a step further? Consider these options:

- **Enable CORS**: If you need cross-origin resource sharing, install `django-cors-headers`:
  ```bash
  pip install django-cors-headers
  ```
  Then, add it to your `INSTALLED_APPS` and middleware in `settings.py`:
  ```python
  INSTALLED_APPS = [
      ...
      'corsheaders',
  ]
  MIDDLEWARE = [
      ...
      'corsheaders.middleware.CorsMiddleware',
  ]
  CORS_ALLOWED_ORIGINS = [
      "http://localhost:3000",
  ]
  ```

- **Optimize database queries**: Use `select_related` and `prefetch_related` in your views to minimize database hits.

### Troubleshooting
If you run into issues, here are some common fixes:

- **Database connection problems**: Make sure PostgreSQL is running and that the credentials in `settings.py` are accurate.
- **Celery not starting**: Check if Redis is running and look for errors in the terminal.
- **API not responding**: Ensure your Django server is running and that the URLs are configured correctly.

### Best Practices
Keep these tips in mind for a smoother development process:

- **Use environment variables**: Store sensitive information, like database credentials, in environment variables.
- **Implement pagination**: Use DRF's pagination classes to handle large datasets efficiently.
- **Write tests**: Develop unit tests for your models and views to ensure everything works as expected.

### Performance Tuning
For better performance, consider:

- **Database indexing**: Add indexes to frequently queried fields in your models.
- **Celery task optimization**: Use task retries and time limits to manage long-running tasks effectively.
- **Static files**: Consider using `whitenoise` or a CDN to serve static files in production.