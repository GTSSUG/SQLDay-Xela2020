# Parte 3: Exponer puertos y manejo de redes
Los controladores de red en Docker en modo host y bridge pueden conectar contenedores en un solo host de docker. Permite que los contenedores se comuniquen más allá de una máquina, permite crear una red de superposición. Los pasos para crear la red dependen de cómo se administran los contenedores y como se desean comunicar entre ellos. 

En este taller trabajaremos con contenedores que se comunicaran en una red interna de Docker y permiten exponer servicios a través de la máquina host.

## Paso 1: Crear una red
Las redes permiten crear segmentos de red virtuales dentro de un host, de tal forma que los contenedores en dicha red se puedan comunicar.
```
docker network create sample
```
## Paso 2: Crear un contenedor sin exponerlo
## Paso 3: Crear un contenedor que se exponga en el puerto 80
## Paso 3: Crear un contenedor que se exponga en el puerto 8080



