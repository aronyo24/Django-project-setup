
# Python Django Static, Media & Templates Configuration

## Overview
This guide explains how to configure:

- **Static files** (CSS, JS, images)  
- **Media files** (user uploads)  
- **Templates** (HTML files)  

in a Django project. It is simple and ready to use for development.

---

## Project Structure (Relevant Parts)
```

django-project-setup/
├── manage.py
├── django_project_setup/
│   ├── settings.py
│   └── urls.py
├── static/       # Store CSS, JS, images here
├── media/        # Store uploaded files here
└── templates/    # Store HTML templates here

````

---

## 1️ Settings in `settings.py`
```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

# Templates configuration
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],  # Path to templates folder
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

# Static files configuration
STATIC_URL = 'static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

# Media files configuration
MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'
````

**Explanation:**

* **Templates:** `DIRS` points to the main `templates` folder. `APP_DIRS=True` allows Django to look for templates inside each app.
* **Static:** `STATIC_URL` is the URL prefix, `STATICFILES_DIRS` is the folder Django looks for static files.
* **Media:** `MEDIA_URL` is the URL prefix, `MEDIA_ROOT` is the directory for uploaded files.

---

## 2️ URLs in `urls.py`

```python
from django.contrib import admin
from django.urls import path
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
]

if settings.DEBUG:
    # Serve static files during development
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATICFILES_DIRS[0])
    # Serve media files during development
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

**Explanation:**

* This allows Django to serve **static and media files in development**.
* In production, serve these via **Nginx** or **Apache**.

---

## 3️ Testing

1. Add a static file: `static/css/style.css`
2. Add a template: `templates/index.html`
3. Upload a media file via Django admin.
4. Run the development server:

```bash
python manage.py runserver
```

5. Open in browser:

   * Static file: `http://127.0.0.1:8000/static/css/style.css`
   * Media file: `http://127.0.0.1:8000/media/<filename>`
   * Template page: `http://127.0.0.1:8000/` (if mapped in views)

---

## Notes

* Keep `DEBUG=True` **only in development**.
* For production, configure `STATIC_ROOT` and serve files via a web server for better performance.
* Always organize templates in the `templates/` folder for clarity.

```
## test
