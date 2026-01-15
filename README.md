# Pasos para Crear un Proyecto en Django con MySQL

### 1.- Creamos a Carpeta donde trabajaremos el Proyecto

### 2.- Creamos el Entorno Virtual Local en Windows (Carpeta Principal)
***
_Importante tener instalado Python 3.12.10 por defecto_
```
python -m venv venv
```
### 3.- Activamos el Entorno Virtual Local en Windows (Carpeta Principal)
***
```
venv\Scripts\activate
```
### 4.- Instalamos el Gestor de Dependencias pip-tools (Carpeta Principal)
***
```
pip install pip-tools
```
_Verificamos_
```
pip-compile --version
```
_Creamos la carpeta requirements y agregamos los .in con las Dependencias (Carpeta Principal)_
---
##### requirements/
##### ├── base.in
##### ├── dev.in
##### └── prod.in
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
### 5.- Creamos el Proyecto
***
```
django-admin startproject config .
```
_Configuración por entornos_
***
config/ \
└── settings/ \
├── __init__.py \
├── base.py \
├── dev.py \
└── prod.py \
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



============================================================

## Table of Contents
1. [General Info](#general-info)
2. [Technologies](#technologies)
3. [Installation](#installation)
4. [Collaboration](#collaboration)
5. [FAQs](#faqs)
### General Info
***
Write down the general informations of your project. It is worth to always put a project status in the Readme file. This is where you can add it. 
### Screenshot
![Image text](https://www.united-internet.de/fileadmin/user_upload/Brands/Downloads/Logo_IONOS_by.jpg)
## Technologies
***
A list of technologies used within the project:
* [Technologie name](https://example.com): Version 12.3 
* [Technologie name](https://example.com): Version 2.34
* [Library name](https://example.com): Version 1234
## Installation
***
A little intro about the installation. 
```
$ git clone https://example.com
$ cd ../path/to/the/file
$ npm install
$ npm start
```
Side information: To use the application in a special environment use ```lorem ipsum``` to start
## Collaboration
***
Give instructions on how to collaborate with your project.
> Maybe you want to write a quote in this part. 
> It should go over several rows?
> This is how you do it.
## FAQs
***
A list of frequently asked questions
1. **This is a question in bold**
Answer of the first question with _italic words_. 
2. __Second question in bold__ 
To answer this question we use an unordered list:
* First point
* Second Point
* Third point
3. **Third question in bold**
Answer of the third question with *italic words*.
4. **Fourth question in bold**
| Headline 1 in the tablehead | Headline 2 in the tablehead | Headline 3 in the tablehead |
|:--------------|:-------------:|--------------:|
| text-align left | text-align center | text-align right |
