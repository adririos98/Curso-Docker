# Curso-Docker
Curso de docker desde cero y para todos.

## - Enlaces de interés.

- https://docs.docker.com/install/linux/docker-ce/ubuntu/
- https://docs.docker.com/compose/
- https://docs.docker.com/machine/

## Introducción a los conceptos de docker.
### Imágenes.
Las imágenes en Docker, es el núcleo de un contenedor, es decir, sin la imagen el contenedor no puede existir. Las imágenes albergan un sistema operativo, una aplicación, un sandbox, etc. Las imágenes se pueden personalizar para crear desarrollos personalizados a nuestras necesidades. Dentro de una imagen podemos indicarle que puerto usar así como la ejecución de un script de requerirse. Multi-stage (Significado: Ejecución de un número determinado de imágenes para obtener una imagen como resultado)

#### Buscar imágenes en el registry oficial de docker.
> docker search [Nombre_imagen] 

#### Docker Hub.
es el repositorio publico que usa Docker para poder descargar imágenes, no obstante también se puede disponer de un registry propio (dockerhub.hi.inet)

* Descargar imagen.
> docker pull [Nombre_imagen] 
* Listar imágenes descargadas.
> docker image ls [Nombre_imagen] 
* Borrar imágenes descargadas.
> docker image rmi [Nombre_imagen]
* Subir imágenes repositorio.
> docker push [Nombre_imagen]  


### Contenedores

Los contenedores son "espacios" donde una aplicación puede "existir" mediante una imagen predeterminada o pre-definida que ha sido llamada para su ejecución como contenedor.
Se puede asignar recursos definidos como el % de CPU, el % de RAM a los contenedores es decir, el número mínimo de recursos y máximo. 

* Para iniciar un contenedor:
> docker run [Nombre_imagen]   
* Para ver el estado de un contenedor: 
> docker ps -a  // docker container ls -a // docker container ps -a 
* Para detener un contenedor:
> docker stop [ID_CONTAINER]
* Para arrancar un contenedor detenido:
> docker start [ID_CONTAINER]
* Para iniciar un contenedor en base a un nombre:
> docker run --name [Nombre_que_queremos_del_Contenedor] [Nombre_imagen]  
* Para iniciar un contenedor en background:
> docker run -dit --name [Nombre_que_queremos_del_Contenedor] [Nombre_imagen]
* Para ver el log de un contenedor: 
> docker logs [ID_CONTAINER]
* Para acceder a un contenedor corriendo en background:
> docker exec -it [ID_CONTAINER]
* Para ejecutar comandos en un contenedor sin llegar a entrar en él:
> docker exec [ID_CONTAINER] mkdir -p /tmp/prueba-epg  
> docker exec [ID_CONTAINER] ls -lta /tmp 
o en una única linea:
> docker exec [ID_CONTAINER] mkdir -p /tmp/prueba-epg  ||  docker exec [ID_CONTAINER] ls -lta /tmp 
* Para eliminar un contenedor:
> docker rm -fv [ID_CONTAINER]
* Para borrar contenedores en una sola linea:
>  docker rm -fv $(docker ps -aq) 
* Para ver el detalle de un contenedor:
> docker inspect [ID_CONTAINER] 