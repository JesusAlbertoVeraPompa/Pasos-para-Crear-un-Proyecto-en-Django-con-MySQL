# Pasos para Crear un Proyecto en Django con MySQL

### 1.- Creamos a Carpeta donde trabajaremos el Proyecto
```
mkdir nombre-carpeta
```
```
cd nombre-carpeta
```

### 2.- Creamos el Entorno Virtual Local en Windows (Carpeta Principal)

_Importante tener instalado Python 3.12.10 por defecto_
```
python -m venv venv
```

### 3.- Activamos el Entorno Virtual Local en Windows (Carpeta Principal)

```
venv\Scripts\activate
```

### 4.- Instalamos el Gestor de Dependencias pip-tools (Carpeta Principal)

```
pip install pip-tools
```

_Verificamos_
```
pip-compile --version
```

_Creamos la carpeta requirements y agregamos los .in con las Dependencias (Carpeta Principal)_

<pre>
requirements/
   └── base.in
</pre>
```
requirements
```
---
```
base.in
```
_base.in_
```
# Core Django / Framework base
django==3.2.25

# Django REST Framework / APIs
djangorestframework==3.15.1

# Variables de entorno / Settings seguros
django-environ

# Biblioteca de bases de datos MySQL
mysqlclient

# JSON Web Tokens (JWT)
djangorestframework-simplejwt

# Filtros para DRF / Filtros en APIs
django-filter

# Manejo de fechas / zonas horarias
pytz
```
---
_Compilamos las Dependencias segun la Necesidad_
```
pip-compile requirements/base.in
```
_Instalamos las Dependencias segun la Necesidad_
```
pip-sync requirements/base.txt
```
---
_Importante Recordar_ \
Editas cualquier requirements\ *.in \
Compilamos
```
pip-compile requirements/*.in
```
Sincronizamos
```
pip-sync requirements/*.txt
```
---
### 5.- Creamos el Proyecto
```
django-admin startproject config .
```

_Configuración del settings por entornos_
<pre>
config/
   └── settings/
         ├── __init__.py
         ├── base.py
         ├── dev.py
         └── prod.py
</pre>

---
```
settings
```
---
```
__init__.py
```
```
base.py
```
_base.py_
```
import os
import sys
import environ
from pathlib import Path
from datetime import timedelta

# ========================================================================
# BASE
# ========================================================================

BASE_DIR = Path(__file__).resolve().parent.parent.parent

env = environ.Env(
    DEBUG=(bool, False)
)

environ.Env.read_env(BASE_DIR / ".env")

# ========================================================================
# SECURITY
# ========================================================================

SECRET_KEY = env("SECRET_KEY")
DEBUG = env("DEBUG")
IS_TESTING = "test" in sys.argv
ALLOWED_HOSTS = []

# ========================================================================
# APPLICATIONS
# ========================================================================

DJANGO_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "corsheaders",
    'drf_spectacular',
]

THIRD_PARTY_APPS = [
    "rest_framework",
    "django_filters",
]

LOCAL_APPS = [
    "apps.usuarios",
    "apps.control_asistencia",
    "apps.pago_proveedores",
    "apps.tareas",
    "rest_framework_simplejwt.token_blacklist",
]

INSTALLED_APPS = DJANGO_APPS + THIRD_PARTY_APPS + LOCAL_APPS

# ========================================================================
# MIDDLEWARE
# ========================================================================

MIDDLEWARE = [
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
]

# ========================================================================
# URLS
# ========================================================================

ROOT_URLCONF = "config.urls"

# ========================================================================
# TEMPLATES
# ========================================================================

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": [BASE_DIR / "templates"],
        "APP_DIRS": True,
        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.debug",
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ],
        },
    },
]

# ========================================================================
# WSGI / ASGI
# ========================================================================

WSGI_APPLICATION = "config.wsgi.application"
ASGI_APPLICATION = "config.asgi.application"

# ========================================================================
# DATABASE (MySQL)
# ========================================================================

DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": env("MYSQL_DATABASE"),
        "USER": env("MYSQL_USER"),
        "PASSWORD": env("MYSQL_PASSWORD"),
        "HOST": env("MYSQL_HOST"),
        "PORT": env("MYSQL_PORT"),
        "OPTIONS": {
            "init_command": "SET sql_mode='STRICT_TRANS_TABLES'"
        },
        "TEST": {
            "MIRROR": "default",
        },
    }
}

# ========================================================================
# AUTH
# ========================================================================

AUTH_PASSWORD_VALIDATORS = [
    {"NAME": "django.contrib.auth.password_validation.UserAttributeSimilarityValidator"},
    {"NAME": "django.contrib.auth.password_validation.MinimumLengthValidator"},
    {"NAME": "django.contrib.auth.password_validation.CommonPasswordValidator"},
    {"NAME": "django.contrib.auth.password_validation.NumericPasswordValidator"},
]

# ========================================================================
# I18N
# ========================================================================

LANGUAGE_CODE = "es-es"
TIME_ZONE = 'America/Bogota'
USE_I18N = True
USE_TZ = True

# ========================================================================
# STATIC / MEDIA
# ========================================================================

STATIC_URL = "/static/"
STATIC_ROOT = BASE_DIR / "staticfiles"

MEDIA_URL = "/media/"
MEDIA_ROOT = BASE_DIR / "media"

DEFAULT_AUTO_FIELD = "django.db.models.BigAutoField"

```
---
```
dev.py
```
_dev.py_
```
from .base import *

DEBUG = True
ALLOWED_HOSTS = []
```
---
```
prod.py
```
_prod.py_
```
from .base import *

DEBUG = False
ALLOWED_HOSTS = ["tudominio.com"]
```
---
### 6.- Creamos las Variables de Entorno (Carpeta Principal)
```
.env
```
```
SECRET_KEY=super-secret-key
DEBUG=True
```
### 7.- Reorganizamos las Carpetas del Proyecto
<pre>
Principal
      ├── apps/
      │      ├── app/
      ├── config/
      │      └── settings/
      ├── logs/
      │      └── error.log
      ├── media/
      ├── requirements/
      ├── services/
      ├── static/
      ├── utils/
      ├── venv/
      ├── .env
      ├── manage.py
      └── README.md
</pre>   
### 8.- Creamos las Apps (Carpeta Principal)
_Ejemplo_
```
python manage.py startapp usuarios apps/usuarios
```
```
python manage.py startapp productos apps/productos
```
