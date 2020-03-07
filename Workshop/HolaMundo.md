# Introducción a Docker
La gente nueva en Docker a menudo no se da cuenta de que los sistemas de archivos de Docker son temporales por defecto. Si inicia una imagen de Docker, obtendrá un contenedor que en la superficie se comporta como una máquina virtual. Puedes crear, modificar y borrar archivos. Sin embargo, a diferencia de una máquina virtual, si detiene el contenedor y lo vuelve a iniciar, todos los cambios se perderán: todos los archivos que eliminó anteriormente volverán y los nuevos archivos o ediciones que haya realizado no estarán presentes.

## Paso 1: Crear un volumen
## Paso 2: Crear un contenedor y configurar un volumen
## Paso 3: Crear una carpeta en los archivos del usuario (actuará como volumen)
## Paso 4: Crear un contenedor y configurar un directorio como volumen
## Paso 5: Crear un contenedor Web y configurar un directorio como volumen (Crear un archivo index.html)