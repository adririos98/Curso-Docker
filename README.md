# Curso-Docker
Curso de docker desde cero y para todos.

## - Enlaces de interés.

- https://docs.docker.com/install/linux/docker-ce/ubuntu/
- https://docs.docker.com/compose/
- https://docs.docker.com/machine/

## 1. Introducción a los conceptos de docker.
### 1.1. Imágenes.
Las imágenes en Docker, es el núcleo de un contenedor, es decir, sin la imagen el contenedor no puede existir. Las imágenes albergan un sistema operativo, una aplicación, un sandbox, etc. Las imágenes se pueden personalizar para crear desarrollos personalizados a nuestras necesidades. Dentro de una imagen podemos indicarle que puerto usar así como la ejecución de un script de requerirse. Multi-stage (Significado: Ejecución de un número determinado de imágenes para obtener una imagen como resultado)

#### 1.1.1. Buscar imágenes en el registry oficial de docker.
> docker search [Nombre_imagen] 

#### 1.1.2. Docker Hub.
es el repositorio publico que usa Docker para poder descargar imágenes, no obstante también se puede disponer de un registry propio (dockerhub.hi.inet)

* Descargar imagen.
> docker pull [Nombre_imagen] 
* Listar imágenes descargadas.
> docker image ls [Nombre_imagen] 
* Borrar imágenes descargadas.
> docker image rmi [Nombre_imagen]
* Subir imágenes repositorio.
> docker push [Nombre_imagen]  


### 1.2 Contenedores.

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
* En una única linea las dos anteriores:
> docker exec [ID_CONTAINER] mkdir -p /tmp/prueba-epg  ||  docker exec [ID_CONTAINER] ls -lta /tmp 
* Para eliminar un contenedor:
> docker rm -fv [ID_CONTAINER]
* Para borrar contenedores en una sola linea:
>  docker rm -fv $(docker ps -aq) 
* Para ver el detalle de un contenedor:
> docker inspect [ID_CONTAINER] 

### 1.3. Red.
En docker se dispone de 3 tipos de redes preconfiguradas para poder ser usadas:

* 1. Bridge: red standard que usarán todos los contenedores.
* 2. Host: el contenedor usará la misma IP del Host.
* 3. None: se utiliza para indicar que un contenedor no tiene asignada una red.

* Para listar las redes que ya se tienen creadas:
> docker network ls 
* Para inspeccionar una red:
> docker network inspect bridge
* Para crear una red nueva:
> docker network create [Nombre_red]

#### ¿Como se usa la red en un contenedor?
Si no se indica el tipo de red, por defecto sera **bridge**

* Para crear una red especifica:
> docker network create --driver **bridge [Nombre_red]**
* Asignamos la red creada a un contenedor:
> docker run -d -P --name [Nombre_contenedor] --network [Nombre_red] [ID_IMAGEN o NOMBRE_IMAGEN] 
* Para eliminar una red:
> docker network delete [Nombre_red]