### Enviar formulario HTML a MySQL con Django

1.  Crear un entorno virtual, hay muchas formas

        Opción 1: Crear entorno virtual con el paquete virtualenv
        Si no tienes instalado virtualenv puedes instalarlo de forma global en el sistema atraves de https://pypi.org/project/virtualenv/
        pip install virtualenv ->Instalar de forma global
        virtualenv env ->Crear entorno
        virtualenv --version ->Ver la versión de virtualenv

        Opción 2: Crear un entorno virtual con el paquete que ya viene por defecto en las ultimas versiones de Python
        python -m venv env

2.  Activar entorno virtual

        . env/Script/activate ->para Windows
        . env/bin/activate -> Para Mac
        deactivate -->Para desactivar mi entorno virtual

3.  Instalar django desde el manejador de paquete de Python Pip, ya dentro del entorno virtual.

        python -m pip install Django
        pip install Django
        Nota: para instalar Django en una version especifica
        pip install Django==4.2.4

4.  Ver la versión de django instalada en el proyecto

        python -m django --version

5.  Crear el proyecto con django

        `django-admin startproject project_core .`
        El punto . es crucial le dice al script que instale Django en el directorio actual

        Ya en este punto se puede correr el proyecto que a creado Django,
        python manage.py runserver

6.  Crear mi primera aplicación en Django

        python manage.py startapp custom_users

7.  Instalar nuestra aplicación (custom_users) ya creada en el proyecto, en el archivo settings.py

        archivo settings.py
        INSTALLED_APPS = [
        ----,
        'custom_users',
        ]

8.  Agregar en el archivo settings.py de la aplicación el siguiente codigo, esto le dirá a nuestra aplicación Django que estamos usando un modelo de usuario persona

        # Authentication
        AUTH_USER_MODEL = "custom_users.CustomUser"
        #custom_users, es el nombre de la aplicación
        #CustomUser, representa la clase de mi modelo el cual personaliza el modelo original de usuario en Django.

9.  Vamos a nuestro modelo de nuestra aplicación custom_users, allí definimos nuestra clase que nos permitirá personalizar el modelo usuario de Django.

        from django.contrib.auth.models import AbstractUser
        from django.db import models

        class CustomUser(AbstractUser):
                first_name = models.CharField(max_length=20, blank=True)
                last_name = models.CharField(max_length=20, blank=True)
                twitter_handle = models.CharField(max_length=20, blank=True)

###### Aquí estamos creando un modelo (una tabla en nuestra BD) que hereda todos los campos de la AbstractUser clase que tiene los campos; username, username, email, password, etc, pero también estamos agregando un par de campos que no están allí. Agregamos los campos: first_name, last_name, twitter_handle

10. Vamos al archivo admin.py agremos este cógido que nos permitira registrar y visualizar nuestra tabla de usuarios en el panel de Django Admin.

        from .models import CustomUser
        admin.site.register(CustomUser)

11. Editar el archivo settings.py del proyecto, cambiando los parametros de conexión a MySQL

        `
        DATABASES = {
                'default': {
                        'ENGINE': 'django.db.backends.mysql', #ENGINE es motor de BD
                        'NAME': 'bd_django_mysql',
                        'USER': 'root',
                        'PASSWORD': '',
                        'HOST': '127.0.0.1',
                        'PORT': '3306',
                }
        }
        `

12. Crear las migraciones y correrlas

        python manage.py makemigrations -> Creando migraciones
        python manage.py migrate         -> Correr migraciones

13. Crear usuario para el login desde la terminal

        python manage.py createsuperuser

14. Correr el proyecto

        python manage.py runserver
        Revisar la consola y visitar la URL http://127.0.0.1:8000

15. Crear el archivo urls.py en la aplicación (bd_django_mysql)

        from django.urls import path
        from . import views

                urlpatterns = [
                        path('', views.inicio, name='inicio'),
                        path('registrar_empleado/', views.registrar_empleado,
                                name='registrar_empleado'),
                        path('empleados/', views.listar_empleados, name='listar_empleados'),
                ]

16. Conectar las URLS de mi aplicación con el projecto, para esto vamos al archivo uls.py del projecto
    from django.urls import path, include

        urlpatterns = [
                path('admin/', admin.site.urls),
                path("", include('empleados.urls'))
        ]

17. Crear la carpeta 'templates' dentro de la aplicación donde estarán mis archivos.html

18. Crear la carpeta 'static' dentro de mi aplicacion, aqui estaran archivos
    estaticos (css, js, imagenes, etc..)

19. Crear la carpeta media, para almacenar las imagenes del empleado

20. Correr archivo requirement.txt

        pip install -r requirements.txt

21. Crear el archivo requirements.txt para tener todos los paquetes del proyecto a la mano

        pip freeze > requirements.txt

        Nota: para instalar los paquetes solo basta ejecutar
        pip install -r requirements.txt

#### Referencias:

https://testdriven.io/blog/django-custom-user-model/

https://docs.djangoproject.com/es/5.0/topics/auth/customizing/

https://www.codingforentrepreneurs.com/blog/how-to-create-a-custom-django-user-model/

https://vegibit.com/how-to-create-custom-user-models-and-authentication-backends-in-django/

#### Resultado final

#####Formulario para registrar Empleado
![](https://raw.githubusercontent.com/urian121/imagenes-proyectos-github/master/registrar-empleado-con-django-crud-urian-viera.png)

##### Lista de Empleados

![](https://raw.githubusercontent.com/urian121/imagenes-proyectos-github/master/lista-de-empleados-crud-django-urian-viera.png)

### Expresiones de Gratitud 🎁

    Comenta a otros sobre este proyecto 📢
    Invita una cerveza 🍺 o un café ☕
    Paypal iamdeveloper86@gmail.com
    Da las gracias públicamente 🤓.

## No olvides SUSCRIBIRTE 👍
