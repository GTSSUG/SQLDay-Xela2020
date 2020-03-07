# Introducción a Docker
Bienvenido a este taller de introduccion a Docker. Esta primera parte te ayudara a comprender los comandos basicos de Docker, utilizaremos el cliente de Docker para realizar tareas como descarga de imagenes, creacion y administracion de containers.

## 1. Como descargar una imagen de Docker

### 1.1. Loguearse a Docker Hub
Como primer paso, debemos loguearnos a Docker Hub utilizando el usuario y password definido al momento de la creacion de la cuenta.

Ejecutemos el siguiente comando:
```bash
docker login
```

### 1.2. Descargar una imagen
Una vez logueados a Docker, tendremos acceso a Docker Hub. Esto nos permite descargar una imagen del repositorio publico, la cual utilizaremos despues para crear un container. 

En el siguiente ejemplo descargaremos la imagen de Alpine:

```bash
docker pull alpine:latest
```
Como puedes ver el comando esta compuesto de dos partes:

>\<nombre imagen> : \<version>

Puedes consultar el listado de imagenes disponible en el repositorio publico [aqui](https://hub.docker.com/search?q=&type=image), a esta combinacion de imagen + version se le llama _tag_.

En nuestro caso, escogimos la ultima version de Alpine. Siendo Alpine la imagen de Docker que nos permite ejecutar una distribucion de Linux muy ligera, la imagen tan solo ocupa 5 MB's.

### 1.3. Listar imagenes

Si queremos consultar el nombre, ID y tamaño de nuestras imagenes descargadas podemos utilizar el siguiente comando:

```bash
docker images alpine
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              e7d92cdc71fe        7 weeks ago         5.59MB
```

## 2. Como crear y administrar un container 

### 2.1. Crear un container
En el siguiente ejemplo utilizaremos la imagen (Alpine) que fue descargada en el paso anterior. El objetivo es crear un container llamado -Xela2020_, con el cual podremos practicar diversas tareas administrativas como detener, iniciar e incluso borrar el container.

A continuacion te presentamos el ejemplo que te ayudar a crear el container:

```bash
docker create -t -i --name xela2020 alpine
caf0015e7588d69cd16199b9e98d6749bf2cc1bf004e4ba2ce68332992899624
```
**Felicitaciones, has creado tu primer container!** No te preocupes si lo unico que viste desplegado en pantalla fue un codigo alfanumerico, esto es simplemente el ID asignado a tu container. Este ID puede ser utilizado para fines administrativos pero en este ejemplo decidimos ponerle un nombre al container (opcional) para hacer mas facil la interaccion utilizando dicho nombre.
 
### 2.2. Consultar el estado de un container
El cliente de Docker se caracteriza por retornar informacion de la manera mas simple posible, por lo cual te preguntaras.
Existe alguna manera de consultar el estado actual de mi container? La respuesta es si, y como es de esperarse con Docker es muy sencillo.

El comando <docker ps> puede ser utilizado para consultar el estado de uno o todos containers existentes en mi implementacion de Docker. Pero dicho comando por default no retornara informacion para containers que esten actualmente detenidos o solo creados. Por lo cual tendremos que utilizar la opcion <-a> la cual nos ayuda a listar todos los containers sin importar su estado.

Ejecuta la siguiente instruccion para consultar el estado de tu container _Xela2020_:

```bash
docker ps -a
CONTAINER ID        IMAGE       COMMAND         CREATED              STATUS         PORTS       NAMES
caf0015e7588        alpine      "/bin/sh"       About a minute ago   Created                    xela2020
```

Como puedes observar, el estado de nuestro container es _Created_ por lo cual confirmamos que fue creado satisfactoriamente.

### 2.3. Iniciar un container
Este paso es bastante sencillo y rapido, nuestro objeto es iniciar el container creado en el paso anteriores. Para esto, utilizaremos el comando <docker start> seguido del nombre de nuestro container _Xela2020_.

```bash
docker start xela2020
xela2020
```
Bastante rapido, verdad? Esta es una de las grandes ventajas de trabajar con containers. El comando nos retorna el nombre de nuestro container afirmando que nuestro container fue iniciado.

### 2.4. Conectarse dentro de un container
Tal y como lo aprendiste el dia de hoy, containers nos permiten crear entornos ligeros de tiempo de ejecución que proporcionan a las aplicaciones los archivos, las variables y las bibliotecas que necesitan para ejecutarse. 

A diferencia de las máquinas virtuales, los contenedores utilizan el sistema operativo (SO) de su host en lugar de proporcionar uno propio. Por lo cual podemos conectarnos dentro de un container tal y como si fuera un host mas.

Para demostrar esto, tendremos que utilizar el comando <docker exec> seguido por las opciones <-it> que simplemente nos permite interactuar con nuestro container utilizand una consola interactiva. En el caso de Linux, vamos a elegir la consola "/bin/bas"

Corre el siguiente comando para conectarte dentro de tu container _Xela2020_:

```bash
docker exec -it xela2020 /bin/sh
/ # 
```
En este momento ya puedes interactuar directamente con tu container, hagamos un ejemplo listando toda las carpetas del path actual utiliznado la instruccion <ls -ll> de Linux:

```bash
/ # ls -ll
total 56
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 bin
drwxr-xr-x    5 root     root           360 Mar  7 06:24 dev
drwxr-xr-x    1 root     root          4096 Mar  7 06:24 etc
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 home
drwxr-xr-x    5 root     root          4096 Jan 16 21:52 lib
drwxr-xr-x    5 root     root          4096 Jan 16 21:52 media
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 mnt
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 opt
dr-xr-xr-x  161 root     root             0 Mar  7 06:24 proc
drwx------    1 root     root          4096 Mar  7 06:27 root
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 run
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 sbin
drwxr-xr-x    2 root     root          4096 Jan 16 21:52 srv
dr-xr-xr-x   13 root     root             0 Mar  7 06:24 sys
drwxrwxrwt    2 root     root          4096 Jan 16 21:52 tmp
drwxr-xr-x    7 root     root          4096 Jan 16 21:52 usr
drwxr-xr-x   12 root     root          4096 Jan 16 21:52 var
```
Ahora intentemos obtener el nombre del host, utilizando el comando <hostname>:

/ # hostname
caf0015e7588

Como puedes ver este nombre es exactamente el mismo que el ID de nuestro container al ejecutar la instruction del ejemplo en la seccion [2.2.](#2.4.-Conectarse-dentro-de-un-container).

Para regresar a la consola de tu maquina personal / laptop, simplemente ejecuta la instruccion <exit>:
27d343e19637
/ # exit

### 2.5. Detener un container
En un momento te podras dar cuenta que no hay mucha diferencia entre iniciar o detener un container. Para proceder con este paso, vamos a utilizar el comando <docker stop> seguido del nombre de nuestro container _Xela2020_.

```bash
docker stop xela2020
```
De nuevo el comando nos retorna el nombre de nuestro container, pero ahora podremos utilizar el comando <docker ps -a> para confirmar que realmente si este detenido:

```bash
docker ps -a
CONTAINER ID        IMAGE       COMMAND         CREATED              STATUS                         PORTS       NAMES
caf0015e7588        alpine      "/bin/sh"       About a minute ago   Exited (137) 11 seconds ago                xela2020
```

### 2.6. Borrar un container
Muy bien! A este punto ya hemos creado, iniciado y detenido nuestro container llamada _Xela2020_. Ahora es el turno de borrarlo, al igual que los ejemplos anteriores este paso es muy sencillo. 

Para esto utilizaremos el comando <docker rm> seguido del nombre de nuestro container _Xela2020_. 

```bash
docker rm xela2020
xela2020
```
Listo! el container fue eliminado de nuestra implementacion de Docker, y una vez mas podemos confirmarlo utilizando <docker ps -a>:

```bash
docker ps -a
CONTAINER ID        IMAGE       COMMAND         CREATED              STATUS                         PORTS       NAMES
```

Como puedes observar, el comando no nos retorna informacion esta vez por lo cual confirmamos que nuestro container _Xela2020_ fue satisfactoriamente borrado.

# Conclusion
Felicidades! Has completado el taller [Introducción a Docker](). Esperamos que haya sido de mucho ayuda, a la vez te invitamos a seguir con el siguiente taller llamado []().