# Creando mi primer hola mundo

La gente nueva en Docker a menudo no se da cuenta de que los sistemas de archivos de Docker son temporales por defecto. Si se inicia una imagen de Docker, obtendrá un contenedor que en la superficie se comporta como una máquina virtual. Puedes crear, modificar y borrar archivos. 

Sin embargo, a diferencia de una máquina virtual, si detiene el contenedor y lo vuelve a iniciar, todos los cambios se perderán: todos los archivos que eliminó anteriormente volverán y los nuevos archivos o ediciones que haya realizado no estarán presentes.

En esta segunda parte del taller trabajaremos con volumenes para persistir información de un contenedor:

## 1- Como crear un volumen
Como primer paso crearemos un volumen de docker.

Ejecutamos el siguiente comando:
```bash
docker volume create datos
```

## 2- Crear un contenedor y configurar un volumen
En este paso creamos un contenedor de Nginx y montamos el volumen de datos en modo solo lectura. Expondremos el contenedor de Nginx a través del puerto 8080 del host local. 

Luego en un navegador web podrás dirigirte a la dirección http://localhost:8080 <- en dependencia del ambiente de docker que estés utilizando.

Ejecutamos el siguiente comando:
```bash
docker run --name HolaMundo1 -p 8080:80 -v datos:/usr/share/nginx/html:ro -d nginx
```

## 3- Eliminar un volumen de datos
Para poder eliminar un volumen de datos es necesario detener el o los contenedores que dependen del volumen de datos y eliminar el o los contenedores que lo utilicen. 

Detenemos el contenedor:

```bash
docker stop HolaMundo1
```

Eliminamos el contenedor:
```bash
docker rm HolaMundo1
```

Para eliminar el volumen puede ejecutar el siguiente comando:

```bash
docker volume rm datos
```



## 4- Crear una carpeta en los archivos del usuario (actuará como volumen)
En ocasiones puede ser de mucha utilidad tener un directorio de fácil acceso para que un contenedor consulte o almacene archivos e información. En la línea de comandos crearemos un directorio para almacenar los archivos del contenedor, crearemos un archivo index.html dentro del directorio que creamos y agregaremos al archivo un "Hola Mundo".

```bash
mkdir datos
cd datos
touch index.html
echo "<html><body><h1>Hola Mundo</h1></body></html>" >> index.html
```

## 5- Crear un contenedor Web y configurar un directorio como volumen
Para finalizar, crearemos un contenedor de Nginx llamado HolaMundo2, expondremos el servicio web del puerto 80 del contenedor al puerto 8080 del host local. Adicionalmente montaremos el directorio que acabamos de montar en modo lectura.

```bash
docker run --name HolaMundo2 -p 8080:80 -v ~/datos:/usr/share/nginx/html:ro -d nginx
```
En un navegador web podrás dirigirte a la dirección http://localhost:8080 y visualizar el "Hola Mundo".

# Conclusion
Felicidades! Has completado el taller [Hola Mundo](./HolaMundo.md). Has aprendido a manejar volumenes y crear contenedores web. Esperamos que haya sido de mucho ayuda, a la vez te invitamos a seguir aprendiendo mucho en este mundo de contenedores!

# ¿Dudas? 
Para más información y registro de este evento click [aqui](https://gtssug-sqlday-xela2020.eventbrite.com).  
Síguenos en [Facebook](https://www.facebook.com/groups/gtssug/) para conocer más acerca de este y otros eventos.

# Síguenos
[![N|Solid](http://dbamastery.com/wp-content/uploads/2018/08/if_twitter_circle_color_107170.png)](https://twitter.com/gtssug) [![N|Solid](http://dbamastery.com/wp-content/uploads/2018/08/if_github_circle_black_107161.png)](https://github.com/GTSSUG)[![N|Solid](http://dbamastery.com/wp-content/uploads/2018/08/if_browser_1055104.png)](https://www.facebook.com/groups/gtssug/)