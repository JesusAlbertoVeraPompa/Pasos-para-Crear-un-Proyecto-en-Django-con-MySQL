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
_Creamos el archivo requirements.in con las Dependencias (Carpeta Principal)_
```
requirements.in
```
```
# Framework principal
django==3.2.25

# REST API
djangorestframework==3.15.1

# Variables de entorno
django-environ

# Biblioteca de bases de datos MySQL
mysqlclient

# JSON Web Tokens (JWT)
djangorestframework-simplejwt

# Cross-Origin Resource Sharing (CORS)
django-cors-headers
```
_Compilamos las Dependencias_
```
pip-compile
```
_Instalamos las Dependencias_
```
pip-sync
```
---
_Importante Recordar_
Editas requirements.in
```
requests
```
Compilamos
```
pip-compile
```
Sincronizamos
```
pip-sync
```
---
