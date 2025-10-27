 ### Django template setup 


## 🧱 Folder Structure

```
templates/
├── base.html
├── includes/
│   ├── header.html
│   └── footer.html
└── pages/
    ├── index.html
    └── about.html
```

---

## ⚙️ settings.py (Reminder)

Make sure Django knows where to find your templates:

```python
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
```

---

## 🧩 base.html

Your main layout file — used by all other pages.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}EduCareSpace{% endblock %}</title>

    <!-- CSS -->
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>

    <!-- Include Header -->
    {% include 'includes/header.html' %}

    <!-- Main Page Content -->
    <main>
        {% block content %}
        {% endblock %}
    </main>

    <!-- Include Footer -->
    {% include 'includes/footer.html' %}

    <!-- JS -->
    <script src="{% static 'js/main.js' %}"></script>
</body>
</html>
```

---

## 🧩 includes/header.html

Reusable navigation bar for all pages.

```html
<header>
    <nav>
        <h1>EduCareSpace</h1>
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/about/">About</a></li>
            <li><a href="/contact/">Contact</a></li>
        </ul>
    </nav>
</header>
<hr>
```

---

## 🧩 includes/footer.html

Footer section that appears on all pages.

```html
<hr>
<footer>
    <p>&copy; 2025 EduCareSpace. All rights reserved.</p>
</footer>
```

---

## 📄 pages/index.html

Example homepage extending `base.html`.

```html
{% extends 'base.html' %}

{% block title %}Home - EduCareSpace{% endblock %}

{% block content %}
<section>
    <h2>Welcome to EduCareSpace</h2>
    <p>Your all-in-one learning management platform built with Django.</p>
</section>
{% endblock %}
```

---

## 📄 pages/about.html

Example **About page** extending the same base template.

```html
{% extends 'base.html' %}

{% block title %}About - EduCareSpace{% endblock %}

{% block content %}
<section>
    <h2>About EduCareSpace</h2>
    <p>
        EduCareSpace is a modern learning management system designed to make education 
        accessible and interactive for everyone. Built with Django, it combines simplicity 
        and performance for teachers and students alike.
    </p>

    <h3>Our Mission</h3>
    <p>
        To empower learners through technology by offering tools that make learning 
        seamless, engaging, and effective.
    </p>

    <h3>Our Vision</h3>
    <p>
        A world where quality education is accessible to all — anytime, anywhere.
    </p>
</section>
{% endblock %}
```

---
