
# Python Django Static & Media Configuration

## Overview
This guide explains how to configure **static files (CSS, JS, images)** and **media files (user uploads)** in a Django project.  
It is simple and ready to use for development.

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

````

---

## 1️⃣ Settings in `settings.py`
```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

# Static files
STATIC_URL = 'static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

# Media files
MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'
````

**Explanation:**

* `STATIC_URL` → URL prefix to access static files.
* `STATICFILES_DIRS` → Folder(s) where Django looks for static files.
* `MEDIA_URL` → URL prefix for media files uploaded by users.
* `MEDIA_ROOT` → Directory where uploaded files are stored.

---

## 2️⃣ URLs in `urls.py`

```python
from django.contrib import admin
from django.urls import path
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
]

if settings.DEBUG:
    # Serve static files
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATICFILES_DIRS[0])
    # Serve media files
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

**Explanation:**

* This allows Django to serve static and media files **during development**.
* In production, static and media files should be served via a web server like **Nginx** or **Apache**.

---

## 3️⃣ Testing

1. Add a static file: `static/css/style.css`
2. Upload a media file via Django admin.
3. Run development server:

```bash
python manage.py runserver
```

4. Open in browser:

   * Static file: `http://127.0.0.1:8000/static/css/style.css`
   * Media file: `http://127.0.0.1:8000/media/<filename>`

---

## Notes

* Keep `DEBUG=True` **only in development**.
* For production, configure `STATIC_ROOT` and serve files via a web server for performance.

---

This configuration ensures **organized and fully functional static and media management** in Django.

```

---

You can **save this file exactly as**:  

```

Python Django static media settings.py config.md

```

---

If you want, I can **also create a fully professional version of `django-project-setup` repo** with this file included, **ready to clone and run**, so you don’t have to configure anything manually.  

Do you want me to do that?
```
