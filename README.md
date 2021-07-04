# Miniproyecto del bloque de administración de sistemas:

El objetivo de este proyecto es desplegar una aplicación tanto a nivel local como en una máquina remota mediante Fabric, Ansible o Docker.

## Despliegue local:

1. Clonar el repositorio con la aplicación:
    Para ello debe introducirse en la consola el siguiente comando, estando siempre dentro del directorio dónde se quiera añadir la aplicación:
    $ git clone https://github.com/caarlosTT/shield.git

2. Crear un entorno virtual en el que se instalarán todos los paquetes y librerias necesarios para ejecutar la aplicación:
    Para ello debe introducirse en la terminal, estando dentro de la carpeta de la aplicación, el siguiente comando:
    $ python3 -m venv .venv
    Para la activación del entorno virtual que se acaba de crear deberá introducirse en la terminal el comando:
    $ source .venv/bin/activate

3. Instalación de los paquetes y librerias necesarios para desplegar la aplicación:
    Para instalar las librerías requeridas para el despliegue de la aplicación en el entorno virtual, debe introducire el siguiente comando mediante el cuál se instalarán las librerias indicadas en el archivo requirements.txt:
    $ pip install -r requirements.txt
    Ha de tenerse en cuenta que el entorno virtual debe estar activado.

4. Realizar las migraciones:
    En el caso de que se hubiese modificado la aplicación en algún aspecto, debe ejecutarse previamente el siguiente comando en la terminal para crear las nuevas migraciones:
    $ python3 manage.py makemigrations
    Para realizar las migraciones necesarias deberá ejecutarse el siguiente comando en la terminal:
    $ python3 manage.py migrate

5. Cargar datos de un fichero:
    Para cargar los datos que utilizará la aplicación, debe ejecutarse en la terminal el siguiente comando, mediante el cuál se cargarán los datos del archivo initial_data.json:
    $ python3 manage.py loaddata metahumans/fixtures/initial_data.json

6. Crear un usuario para la administración de la aplicación:
    Cada vez que se quiera crear un nuevo usuario para administrar la aplicación una vez esta esté desplegada deberá introducirse en la terminal el siguiente comando:
    $ python3 manage.py create superuser
    Posteriormente deberá introducirse el nombre, correo y contraseña de dicho usurio en la terminal, según sean requeridos dichos datos.

7. Despliegue de la aplicación:
    Finalmente, para desplegar la aplicación en local, deberá introducirse en la terminal el siguiente comando:
    $ python3 manage.py runserver
    En la misma terminal aparecerá un link que deberá introducirse en un explorador web y mediante el cuál accederemos a la página inicial de la aplicación.
    Si la página no cuenta de una vista para la página inicial, deberá añadirse al link la url de alguna de las vistas que se indique que si están disponibles.

## Despliegue en una máquina remota mediante Fabric:

1. Instalación de Fabric:
    Deberá introducirse en la terminal el siguiente comando, teniendo el entorno virtual activado:
    $ pip install fabric

2. Dirección del repositorio de la aplicación:
    Deberá comprobarese la dirección del repositorio que aparece en la línea 8
    del documento fabfile.py. Dicha dirección deberá ser la del repositorio desde el cuál se clonará la aplicación.

3. Datos de la maquina remota:
    Los datos del nombre, dirección IP y contraseña de la máquina remota en la que se desplegará la aplicación, deberán indicarse en las líneas 14, 15 y 16 del del documento fabfile.py.

    Las tareas que se realizarán en la máquina remota están indicadas a continuación y siguen los mismos pasos que en el despliegue local.

4. Activación de la máquina remota:
    La máquina sobre la cuál vaya a desplegarse la aplicación deberá estar operativa para poder conectar con ella.

6. Despliegue de la aplicación en la máquina remota:
    Para desplegar la aplicación deberá introducirse en la terminal, estando dentro del directorio dónde se encuentra el documento fabfile.py, el siguiente comando:
    $ fab development deploy

## Despliegue en una máquina remota mediante Ansible:

1. Instalación de Ansible:
    Debe introducirse en la terminal, estando activado el entorno virtual el siguiente comando:
    $ pip install ansible

1. Introducir datos de la máquina:
    Debe indicarse la dirección IP de la máquina sobre la cuál vaya a desplegarse la aplicación en el documento hosts.

2. Las acciones que se realizarán en la máquina remota están en los documentos provision.yml y deploy.yml.

3. Despliegue de la aplicación:
    Para desplegar la aplicación en la máquina remota deberá introducirse en la terminal el siguiente comando:
    ansible-playbook -i hosts provision.yml --user=vagrant --ask-pass

    Con este comando se ejecutará tanto el documento provision.yml como deploy.yml.

## Despliegue en una máquina remota mediante Docker:

1. Instalación de Docker:
    Debe introducirse en la terminal, estando activado el entorno virtual el siguiente comando:
    $ pip install ansible

2. Construcción de una imagen:
    Para construir una imagen de la aplicación deberá ejecutarse en la terminal el siguiente comando:
    $ docker build

3. Correr la imagen en un contenedor:
    Para correr la imagen que se acaba de crear en un contenedor deberá introducirse en la terminal el siguiente comando:
    $ docker run -d -p 8000:8000 python-docker

    De esta forma, al introducir la url de la aplicación flask en el navegador, la aplicación será visible en la red local y además podrá modificarse de forma asíncrona.