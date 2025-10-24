
## **1️⃣ Django project Setup**


## **2️⃣ Project Folder Structure**

```
django-starter-kit/
├── manage.py
├── django_starter_kit/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── apps/
│   └── example_app/
│       ├── __init__.py
│       ├── admin.py
│       ├── apps.py
│       ├── models.py
│       ├── tests.py
│       └── views.py
├── templates/
├── static/
├── media/
├── requirements.txt
├── .gitignore
├── .env
└── README.md
```

* `apps/` → Keep all your Django apps here.
* `templates/` → HTML templates.
* `static/` → CSS, JS, images.
* `media/` → User-uploaded files.

---

## **3️⃣ Git Configuration**

### **.gitignore**

```gitignore
# Python
*.pyc
__pycache__/
*.pyo

# Virtual environment
env/
*.env
.venv/

# Django
db.sqlite3
/staticfiles/
/media/

# IDE / OS
.vscode/
.DS_Store
Thumbs.db
```

---

## **4️⃣ Environment Variables (.env)**

```dotenv
SECRET_KEY=your_django_secret_key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
DB_NAME=your_db_name
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_HOST=localhost
DB_PORT=5432
```

### **Load in `settings.py` using `python-decouple`:**

```python
from decouple import config

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=True, cast=bool)
ALLOWED_HOSTS = config('ALLOWED_HOSTS', default='localhost').split(',')

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST', default='localhost'),
        'PORT': config('DB_PORT', default='5432'),
    }
}
```

---

## **5️⃣ Dependencies**

### `requirements.txt` (basic setup)

```
Django>=4.2
python-decouple
psycopg2-binary  # If using PostgreSQL
djangorestframework  # Optional if using APIs
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---



## Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/django-starter-kit.git
cd django-starter-kit
````

### 2. Create Virtual Environment

```bash
python -m venv env
source env/bin/activate      # Linux/Mac
env\Scripts\activate         # Windows
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create `.env` file as shown above.

### 5. Database Setup

```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Create Superuser

```bash
python manage.py createsuperuser
```

### 7. Run Development Server

```bash
python manage.py runserver
```

---

## Git Setup

```bash
git init
git add .
git commit -m "Initial commit - Django Starter Kit"
git branch -M main
git remote add origin https://github.com/yourusername/django-starter-kit.git
git push -u origin main
```

---

## Optional Configurations

### Static & Media Files

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / "static"]
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / "media"
```

### Production Tips

* Set `DEBUG=False`
* Configure proper `ALLOWED_HOSTS`
* Use PostgreSQL or MySQL in production
* Serve static files via Nginx/Apache

