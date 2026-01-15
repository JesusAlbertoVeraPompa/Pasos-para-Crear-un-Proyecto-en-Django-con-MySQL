# Pasos para Crear un Proyecto en Django con MySQL

## 1.- Creamos a Carpeta donde trabajaremos el Proyecto

## 2.- Creamos el Entorno Virtual Local en Windows (Carpeta Principal)
_Importante tener instalado Python 3.12.10_
```
python -m venv venv
```
## 3.- Activamos el Entorno Virtual Local en Windows (Carpeta Principal)
```
venv\Scripts\activate
```
## 4.- Instalamos el Gestor de Dependencias pip-tools (Carpeta Principal)
```
pip install pip-tools
```
_Verificamos_
```
pip-compile --version
```
_Creamos la carpeta requirements y agregamos los .in con las Dependencias (Carpeta Principal)_
---
requirements/ \
├── base.in  \
├── dev.in  \
└── prod.in  \
---
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
