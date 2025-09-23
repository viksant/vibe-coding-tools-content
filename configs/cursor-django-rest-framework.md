---
title: "Enhanced Cursor Django REST Framework Configuration"
description: "Comprehensive setup for Django REST API development with DRF, PostgreSQL, and Celery integration."
category: "configuration"
tags: ["cursor", "django", "rest-framework", "api", "postgresql", "python", "celery", "redis"]
tech_stack: ["python", "django", "drf", "postgresql", "redis", "celery"]
---

This configuration provides a comprehensive setup for Django REST API development with DRF, PostgreSQL, and Celery integration.

### Configuration Overview
This setup enables the development of robust RESTful APIs using Django REST Framework (DRF) with PostgreSQL as the database and Celery for asynchronous task processing.

### Prerequisites
- Python 3.8 or higher
- Django 3.2 or higher
- Django REST Framework 3.12 or higher
- PostgreSQL 12 or higher
- Redis (for Celery)
- pip (Python package installer)

### Installation & Setup
1. **Create a new Django project**:
   ```bash
   django-admin startproject myproject
   cd myproject
   ```

2. **Install required packages**:
   ```bash
   pip install django djangorestframework psycopg2-binary celery redis
   ```

3. **Create a new Django app**:
   ```bash
   python manage.py startapp myapp
   ```

4. **Add the app and DRF to `settings.py`**:
   ```python
   INSTALLED_APPS = [
       ...
       'rest_framework',
       'myapp',
   ]
   ```

5. **Configure PostgreSQL database in `settings.py`**:
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

9. **Create a serializer in `myapp/serializers.py`**:
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

12. **Include app URLs in `myproject/urls.py`**:
    ```python
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('api/', include('myapp.urls')),
    ]
    ```

13. **Run migrations**:
    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```

14. **Start the Django server**:
    ```bash
    python manage.py runserver
    ```

15. **Start the Celery worker**:
    ```bash
    celery -A myproject worker --loglevel=info
    ```

### File Structure
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
- **`settings.py`**: Contains database and Celery configurations.
- **`celery.py`**: Initializes Celery with Django settings.
- **`models.py`**: Defines database models.
- **`serializers.py`**: Maps models to JSON format.
- **`views.py`**: Implements API logic.

### Advanced Options
- **Enable CORS**: Install `django-cors-headers` for cross-origin resource sharing.
  ```bash
  pip install django-cors-headers
  ```
  Add to `INSTALLED_APPS` and middleware in `settings.py`:
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

- **Optimize database queries**: Use `select_related` and `prefetch_related` in your views to reduce database hits.

### Troubleshooting
- **Database connection issues**: Ensure PostgreSQL is running and credentials in `settings.py` are correct.
- **Celery not starting**: Verify Redis is running and check for errors in the terminal.
- **API not responding**: Check if the Django server is running and URLs are correctly configured.

### Best Practices
- **Use environment variables**: Store sensitive information like database credentials in environment variables.
- **Implement pagination**: Use DRF's pagination classes to handle large datasets.
- **Write tests**: Create unit tests for your models and views to ensure reliability.

### Performance Tuning
- **Database indexing**: Add indexes to frequently queried fields in your models.
- **Celery task optimization**: Use task retries and time limits to manage long-running tasks effectively.
- **Static files**: Use `whitenoise` or a CDN for serving static files in production.