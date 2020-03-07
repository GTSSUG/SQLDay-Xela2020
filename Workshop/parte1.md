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

### 2.4. Detener un container
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

### 2.5. Borrar un container
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