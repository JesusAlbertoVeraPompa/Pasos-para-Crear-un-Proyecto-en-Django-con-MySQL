# Pasos para Crear un Proyecto en Django con MySQL

### 1.- Creamos a Carpeta donde trabajaremos el Proyecto

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
   ├── base.in
   ├── dev.in
   └── prod.in
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
```
dev.in
```
_dev.in_
```
-r base.in

# Debug / Ver SQL, cache, performance
django-debug-toolbar

# Testing / Testing moderno
pytest
pytest-django
factory-boy
faker

# Linting / calidad
black
flake8
isort

# Utilidades
ipython
```
---
```
prod.in
```
_prod.in_
```
-r base.in

# Servidor WSGI / Servidor de producción
gunicorn

# Seguridad / headers / APIs públicas
django-cors-headers

# Cache / performance
redis

# Static files
whitenoise

# Monitoreo de errores
sentry-sdk
```
---
_Compilamos las Dependencias segun la Necesidad_
```
pip-compile requirements/base.in
```
```
pip-compile requirements/dev.in
```
```
pip-compile requirements/prod.in
```
_Instalamos las Dependencias segun la Necesidad_
```
pip-sync requirements/base.txt
```
```
pip-sync requirements/dev.txt
```
```
pip-sync requirements/prod.txt
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
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    ...
]

MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    ...
]
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
### 7.- Creamos las Apps (Carpeta Principal)
_Ejemplo_
```
python manage.py startapp users
```
```
python manage.py startapp products
```
### 8.- Reorganizamos las Carpetas del Proyecto
<pre>
Principal
      ├── apps/
      │      ├── users/
      │      └── products/
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
