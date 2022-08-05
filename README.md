# Curso-Docker
Curso de docker desde cero y para todos.

## - Enlaces de interés.

- https://docs.docker.com/install/linux/docker-ce/ubuntu/
- https://docs.docker.com/compose/
- https://docs.docker.com/machine/
- https://docs.docker.com/engine/reference/commandline/docker/

## 1. Introducción a los conceptos de docker. [NOVATO]
### 1.1. Imágenes.
Las imágenes en Docker, es el núcleo de un contenedor, es decir, sin la imagen el contenedor no puede existir. Las imágenes albergan un sistema operativo, una aplicación, un sandbox, etc. Las imágenes se pueden personalizar para crear desarrollos personalizados a nuestras necesidades. Dentro de una imagen podemos indicarle que puerto usar así como la ejecución de un script de requerirse. Multi-stage (Significado: Ejecución de un número determinado de imágenes para obtener una imagen como resultado)

#### 1.1.1. Buscar imágenes en el registry oficial de docker.
> docker search [Nombre_imagen] 

#### 1.1.2. Docker Hub.
Es el repositorio publico que usa Docker para poder descargar imágenes, no obstante también se puede disponer de un registry propio (dockerhub.hi.inet)

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

### 1.3. Puertos.
* Conectarse al contenedor por un puerto local del equipo anfitrión.
> docker container run -d -p 8080:80 nginx
* Asignar puertos aleatorios a un contenedor.
> docker container run -d -P nginx
* Mostrar varios puertos.
> docker container run -d -p 8080:80 -p 3001:3000 -p 2222:2222 nginx (**Tener cuidado con el puerto 22**)
* Listar puertos abiertos de un contenedor.
> docker container port [ID_CONTENEDOR]


### 1.4. Red.
En docker se dispone de 3 tipos de redes preconfiguradas para poder ser usadas:

* 1. Bridge: red standard que usarán todos los contenedores.
* 2. Host: el contenedor usará la misma IP del Host.
* 3. None: se utiliza para indicar que un contenedor no tiene asignada una red.

* Para listar las redes que ya se tienen creadas:
> docker network ls 
* Para inspeccionar una red:
> docker network inspect [Nombre_red]
* Para crear una red nueva:
> docker network create [Nombre_red]

#### 1.4.1. ¿Como se usa la red en un contenedor?
Si no se indica el tipo de red, por defecto sera **bridge**

* Para crear una red especifica:
> docker network create --driver **bridge [Nombre_red]**
* Asignamos la red creada a un contenedor:
> docker run -d -P --name [Nombre_contenedor] --network [Nombre_red] [ID_IMAGEN o NOMBRE_IMAGEN] 
* EJ:
> docker run -d -P --name pruebanginx --network [Nombre_red] nginx
* Para eliminar una red:
> docker network delete [Nombre_red]

### 1.5. Volúmenes.
En este apartado hablaremos sobre lo tipos de volúmenes existentes en docker, hay 3 tipos de volúmenes:

* Volumen: es la manera sencilla y predefinida para almacenar todos los ficheros en un contenedor, usa el espacio de Host en **/var/lib/docker/volumes** y crea una carpeta para cada contenedor.

* Para crear un volume:
> docker volume create [NOMBRE_VOLUMEN]
* Para asignar el volume creado a un contenedor:
> docker run -d -it --name [NOMBRE_CONTENEDOR] -v [NOMBRE_VOLUMEN]:[/RUTA/CONTENEDOR] [NOMBRE_IMAGEN]

* Volumen bind: es una manera de asociar una carpeta de nuestro Host y conectarla como una carpeta dentro de un contenedor.
Este sistema nos permite ver esa carpeta desde el contenedor y también desde nuestro Host. Usar esos ficheros, copiarlos y además en caso de tener una solución de almacenamiento distribuido, poder tener múltiples copias.
* Ejemplo:
> docker run -d -it --name [NOMBRE_CONTENEDOR] -v [/RUTA/FÍSICA]:[/RUTA/CONTENEDOR] [NOMBRE_IMAGEN]

* TMPFS (temporal file system): es una manera de montar carpetas temporales en un contenedor. Usan la RAM del equipo y su contenido desaparecerá al parar el contenedor.

* Ejemplo:
> docker run -d -it --name [NOMBRE_CONTENEDOR] --tmpfs [/RUTA/TEMPORAL] [NOMBRE_IMAGEN]

#### 1.5.1 Copiar ficheros a un contenedor.
* Copiar ficheros desde un contenedor al equipo físico.
> docker cp [ID_CONTAINER:RUTA_CONTENEDOR] [RUTA_HOST_FISICO]
* Copiar desde Host físico hasta el contenedor.
> docker cp [RUTA_HOST_FISICO] [ID_CONTAINER:RUTA_CONTENEDOR] 


### 1.6 Personalizando una imagen a nuestro gusto.
Un Dockerfile es un archivo de texto plano que contiene una serie de instrucciones necesarias para crear una imagen que, posteriormente, se convertirá en una sola aplicación utilizada para un determinado propósito.

Es como la receta necesaria para un banquete, en este caso el Dockerfile es necesario para la imagen que queramos construir, el Dockerfile es la receta y el gran banquete será nuestra imagen.

``` bash
# Descarga la imagen de Ubuntu 22.04
FROM ubuntu:22.04
# Mantenedor del contenedor
MAINTAINER AdriánHernándezRios adrian.sevilla@dockercurso.com
# Actualiza la imagen base de Ubuntu 14.04
RUN apt-get update
# Definir ambiente de entorno
ENV PRUEBAVAR valorholaEQUIPO
# Instalar Git
RUN apt-get -qqy install git
# Ejecuta el commando apt-get install y elimina determinados archivos y temporales
RUN apt-get install -y nginx \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# Indica los puertos TCP/IP los cuales se pueden accede a los servicios del contenedor
EXPOSE 80
# Establece el commando del proceso de inicio del contenedor
CMD [“nginx”]
```
### EJERCICIOS FINALES. INTRODUCCIÓN. 
**Guarda todos los comandos y salidas mostradas de tu consola.**

#### EJERCICIO 1. Personalizar un contenedor que se encuentra corriendo.
1. Hacer correr un contenedor ubuntu.
2. Acceder al contenedor.
3. Crear un fichero en /tmp.
4. Generar una imagen del contenedor mientras se encuentra corriendo. (**docker commit [ID_CONTENEDOR]**)
5. Asignar un nombre a la imagen creada. (**docker tag [ID_IMAGEN] [NOMBRE:ETIQUETA]**)
6. Probar que el fichero existe en esta nueva imagen.

#### EJERCICIO 2. Personalizar un contenedor mediante dockerfile y acceder a él.
 a) Realizar una imagen mediante dockerfile. (Nombre del fichero **Dockerfilelabs-[TUNOMBRE]**)
- Debe contener 4 variables definidas en el dockerfile (*Las que quieras*)
- Debe exponer el puerto 80 y 443
- Debe tener instalado git y curl.
 
 b) Averiguar el comando para generar la imagen a partir de un fichero de dockerfile. **[INVESTIGACIÓN]**
    
> docker build --file [Nombre_fichero] -t [NOMBRE_IMAGEN:ETIQUETA] . 
 
 c) Crear un contenedor con la imagen creada.


#### CONFIGURAR ACCESO A UN REGISTRY PRIVADO Y ACCEDER.
[Ejercicio de investigación]

#### EJERCICIO 3. Resolver KAHOOT.
[Test Introducción Docker](**PENDIENTE**)


## 2. Level UP - DOCKER-COMPOSE. [INTERMEDIO]
herramienta para definir y ejecutar aplicaciones Docker multicontenedor que permite simplificar el uso de Docker a partir de archivos YAML, de está forma es mas sencillo crear contenedores que se relacionen entre sí, conectarlos, habilitar puertos, volúmenes, etc. Nos permite lanzar un solo comando para crear e iniciar todos los servicios desde su configuración(YAML), esto significa que puedes crear diferentes contenedores y al mismo tiempo diferentes servicios en cada contenedor, integrarlos a un volumen común e iniciarlos y/o apagarlos, etc. Este es un componente fundamental para poder construir aplicaciones y microservicios.
Docker-Compose funciona en todos los entornos: production, staging, development, testing, así como flujos de trabajo basados en Continuous Integration(CI).

## EJERCICIO 0: Instalar docker-compose.
[Investigación]

## EJERCICIO 1: Despliegue contenedor web y database

En la carpeta **2.Docker-compose/Soluciones/EJERCICIO1**, tenemos el fichero *docker-compose.yml* quien orquestará toda la creación de contenedores que necesitemos, para ello debemos ejecutar el comando: 

>**docker-compose up -d**

Lo que realizara *docker-compose.yml* es aquí el tremendo potencial que tiene, y es la sintaxis **build**, pues mediante docker-compose podemos indicarle que lea un Dockerfile, caso contrario podemos usar **image** para que pueda usar la imagen descargada en nuestro Host. La sintaxis **container_name** asigna un nombre a nuestro contenedor, **enviroment** sirve para setear las variables de entorno, para nuestro caso, passwd, user para mariadb, la sintaxis **volume** asigno el mismo al contendor.

### OBS.

* Para visualizar la web, vamos a ingresar via un browser, colocando la IP Publica.

* Si al acceder a la Web, nos encontramos con un Forbiden ( 403 ), debemos entrar al contenedor y crear un **index.html**

> docker exec -it ID_CONTAINER bash
> touch index.html /var/www/html/

## EJERCICIO 2

Modificar nuestro docker-compose, en esta linea:
**sg1:/var/www/html:rw**
por el valor:
**sg1:/var/www/html:ro**

Levantar de nuevo el compose.

> docker-compose up -d

Ahora se va a copiar la carpeta que se encuentra en EJERCICIO2 llamada web en el contenedor, para ello vamos a usar el comando:

> **docker cp web/.  web_apache:/var/www/html**

¿A qué se debe el mensaje de error?

**Error response from daemon: mounted volume is marked read-only**

Al declarar el volumen como RO (Red-Only), no se dispone de permisos de escritura en el contenedor.

### SOLUCIÓN:
- Copiar la data desde el HOST hacia el volumen creado.
- La segunda opción es cambiar en el fichero de *docker-compose* los valores nuevamente y dejarlo con RW.

Ejecutamos el compose de nuevo: 
> **docker-compose up -d**
> docker cp web/. web_apache:/var/www/html


## EJERCICIO PARA PRACTICAR DEL 3 y 4.
El resto de ejercicios es para poner en práctica todo lo aprendido y ver muchas opciones diferentes de configuración a nivel de docker-compose.

## 3. Level TOP - DOCKER SWARM. [EXPERTO] 
**ESTE APARTADO ES OPCIONAL. ESTA DISEÑADO PARA TODOS AQUELLOS QUE QUIERAN SEGUIR APRENDIENDO SOBRE DOCKER Y SU SOLUCIÓN DE CLUSTER.**

Es una herramienta que permite a los desarrolladores implementar contenedores en modo swarm. Un clúster Swarm consiste en Docker Engine implementado en múltiples nodos. Los nodos de administración realizan la orquestación y la administración del clúster. Los nodos de trabajo reciben y ejecutan tareas desde los nodos de administración.

Un servicio consiste en tareas que puedes ejecutarse en nodos de Swarm. Los servicios se pueden replicar para ejecutarse en multiples nodos. En el modelo de servicio replicados, el equilibrio de carga de ingreso y el DNS internos se pueden usar para proporcionar puntos finales de servicio altamente disponibles.

- Para la instalación de docker swarm, se va a emplear docker-machine con virtualbox

```shell
# creación maquinas de ejemplo con docker machine
docker-machine create -d virtualbox manager1

Running pre-create checks...
Creating machine...
(manager1) Copying /home/usuario/.docker/machine/cache/boot2docker.iso to /home/usuario/.docker/machine/machines/manager1/boot2docker.iso...
(manager1) Creating VirtualBox VM...
(manager1) Creating SSH key...
(manager1) Starting the VM...
(manager1) Check network to re-create if needed...
(manager1) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env manager1

# creación resto maquinas
docker-machine create -d virtualbox worker1
docker-machine create -d virtualbox worker2

# lista maquinas creadas
docker-machine ls 
NAME       ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER     ERRORS
manager1   -        virtualbox   Running   tcp://192.168.33.102:2376           v20.10.17   
worker1    -        virtualbox   Running   tcp://192.168.33.103:2376           v20.10.17   
worker2    -        virtualbox   Running   tcp://192.168.33.104:2376           v20.10.17 


- Swarm con maquinas virtuales en ejecución

```shell
# acceder a maquina manager1 por ssh
docker-machine ssh manager1
docker@manager1:~$ 

# ejecución init swarm en maquina actual (ip 192.168.33.102)
docker@manager1:~$ docker swarm init --advertise-addr 192.168.33.102

Swarm initialized: current node (7tn2zpmalg5cye47kdloy26ns) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3tisudabghsdbkyhwbkqwiuyfqewinciqe35itnf3u55tb4ubf-56qpñlo25a3ikr47yendlfypu 192.168.33.102:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

docker@manager1:~$ exit
logout

# agregar workers al swarm del manager previo
docker-machine ssh worker1
docker@worker1:~$ 

# agregar sentencia para agregarse al nodo de la maquina manager
docker@worker1:~$ docker swarm join --token SWMTKN-1-3tisudabghsdbkyhwbkqwiuyfqewinciqe35itnf3u55tb4ubf-56qpñlo25a3ikr47yendlfypu 192.168.33.102:2377

This node joined a swarm as a worker.

docker@worker1:~$ exit
logout

docker-machine ssh worker2
docker@worker2:~$ 

# agregar sentencia para agregarse al nodo de la maquina manager
docker@worker2:~$ docker swarm join --token SWMTKN-1-3tisudabghsdbkyhwbkqwiuyfqewinciqe35itnf3u55tb4ubf-56qpñlo25a3ikr47yendlfypu 192.168.33.102:2377

This node joined a swarm as a worker.

docker@worker2:~$ exit
logout
```

- Gestion Swarm desde el manager 

```shell
# acceder a maquina manager1 por ssh
docker-machine ssh manager1

# ver nodos
docker node ls

ID                            HOSTNAME     STATUS    AVAILABILITY     MANAGER STATUS      ENGINE VERSION
7tn2zpmalg5cye47kdloy26ns *   manager1     Ready     Active           Leader              20.10.17
gyg6ros9ft2jqpkizlwscv583     worker1      Ready     Active                               20.10.17
i38hw0fjukjnvdlvdt8hpsith     worker2      Ready     Active                               20.10.17
```

## Ejemplo de YAML.

``` yaml

version: '3.2'
services:
  wso2eiana-worker:
    image: docker.wso2.com/wso2ei-analytics-worker:6.6.0.107
    deploy:
      placement:
         constraints: [node.hostname == PEPELIDESWSO2EI01]
      replicas: 1
      resources:
        limits:
          cpus: '0.7'
          memory: 1024M
        reservations:
          cpus: '0.2'
          memory: 512M
    hostname: worker
    ports:
      - 9091:9091
      - 9444:9444
      - 7612:7612
      - 7712:7712
      - 7070:7070
      - 7443:7443
    volumes:
      # mounting configurations
      - /opt/wso2_ei_6.6/docker-compose/integrator-analytics-DES/worker:/home/wso2carbon/wso2-config-volume
      - /var/log/wso2ei/worker:/home/wso2carbon/wso2ei-6.6.0/wso2/analytics/wso2/worker/logs
      - /opt/wso2_ei_6.6/certificados/DES:/home/wso2carbon/wso2ei-6.6.0/wso2/analytics/resources/security
    env_file:
      - ../vars/varsDES.env
    environment:
      - TZ=Europe/Madrid
    secrets:
      - PASSBD_EI_ANALYTICS

  wso2eiana-dashboard:
    image: docker.wso2.com/wso2ei-analytics-dashboard:6.6.0.107
    deploy:
      placement:
         constraints: [node.hostname == PEPELIDESWSO2EI01]
      replicas: 1
      resources:
        limits:
          cpus: '0.7'
          memory: 1024M
        reservations:
          cpus: '0.2'
          memory: 512M
    hostname: dashboard
    ports:
      - 9643:9643
      - 9611:9611
      - 9711:9711
    env_file:
      - ../vars/varsDES.env
    environment:
      - TZ=Europe/Madrid
    volumes:
      - /opt/wso2_ei_6.6/docker-compose/integrator-analytics-DES/dashboard:/home/wso2carbon/wso2-config-volume
      - /var/log/wso2ei/dashboard:/home/wso2carbon/wso2ei-6.6.0/wso2/analytics/wso2/dashboard/logs
      - /opt/wso2_ei_6.6/certificados/DES:/home/wso2carbon/wso2ei-6.6.0/wso2/analytics/resources/security
    secrets:
      - PASSBD_EI_ANALYTICS
      - PASSBD_ANALYTICS_DASHBOARD
      - PASSBD_ANALYTICS_PERMISSIONS
      - PASS_EI

  wso2ei-nodo01:
    image: docker.wso2.com/wso2ei-integrator:6.6.0.107
    deploy:
      placement:
         constraints: [node.hostname == PEPELISWSO2EI01]
      replicas: 1
      resources:
        limits:
          cpus: '1.6'
          memory: 4096M
        reservations:
          cpus: '0.5'
          memory: 1024M
    hostname: nodo01
    command: 
      - chmod 777 /home/wso2carbon/docker-entrypoint.sh; chmod +x /home/wso2carbon/docker-entrypoint.sh; chown wso2carbon:wso2carbon /home/wso2carbon/docker-entrypoint.sh 
    ports:
      - target: 9443
        published: 9443
        protocol: tcp
        mode: host
      - target: 8243
        published: 8243
        protocol: tcp
        mode: host
      - target: 8280
        published: 8280
        protocol: tcp
        mode: host
      - target: 4100
        published: 4100
        protocol: tcp
        mode: host
    volumes:
      # mounting configurations
      - /opt/wso2_ei_6.6/docker-compose/integrator-analytics-DES/integrator01:/home/wso2carbon/wso2-config-volume/
      - /opt/nfs/wso2/nfs-server:/home/wso2carbon/nfs-server/
      - /opt/wso2_ei_6.6/datos_del_nfs_compartido/docker-entrypoint/docker-entrypoint.sh:/home/wso2carbon/docker-entrypoint.sh
      - /var/log/wso2ei:/home/wso2carbon/wso2ei-6.6.0/repository/logs
      #- /opt/wso2_ei6.6-analytics/certificados/DES:/home/wso2carbon/wso2ei-6.6.0/repository/resources/security
      - /opt/wso2_ei_6.6/certificados/DES:/home/wso2carbon/wso2ei-6.6.0/repository/resources/security
    env_file:
      - ../vars/varsDES.env
    environment:
      - TZ=Europe/Madrid
    depends_on:
      - wso2eiana-worker
      - wso2eiana-dashboard
    secrets:
      - PASS_CarbonDB_01
      - PASS_CarbonDB_02
      - PASS_WSO2RegistryDB
      - PASS_WSO2UMDB
      - PASS_EI
      - PASS_ANALYTICS

secrets:
  PASS_CarbonDB_01:
    external: true
  PASS_CarbonDB_02:
    external: true
  PASS_WSO2UMDB:
    external: true
  PASS_WSO2RegistryDB:
    external: true
  PASS_EI:
    external: true
  PASSBD_EI_ANALYTICS:
    external: true
  PASS_ANALYTICS:
    external: true
  PASSBD_ANALYTICS_DASHBOARD:
    external: true  
  PASSBD_ANALYTICS_PERMISSIONS:
    external: true


```


## Ejercicios Docker-Swarm

### Ejercicio 1 

Vamos a desplegar una aplicación básico, usar Nginx como imagen base y vamos a iniciarlo con 3 replicas:

> docker service create **--name webnginx** --replicas 3 nginx 

Donde: 

- name: Nombre para el contenedor.
- replicas: Cantidad de replicas que se desea disponer.
- nginx: Nombre de la imagen.

Para listar los servicios creados usamos:

> docker service ls 

Para saber la cantidad de réplicas y donde están distribuidas:

> docker service ps [ID_CONTENEDOR]

Desde el nodo master, ejecutar:

> docker inspect [ID_CONTENEDOR] | grep IPA 

> curl [IP_CONTENEDOR]  

Como podemos observar, tenemos **Nginx** en funcionamiento, pero no es muy accesible que digamos, porque solo "vive" en la red de Docker. 

### Ejercicio 2

Vamos ahora modificar esa limitante, para ello recurrimos al siguiente comando: 

> docker service **update** **--publish-add 9090:80**  webnginx

donde: 

- update: Comando a usar para modificar un servicio.
- publish-add: Puertos **Host/Contenedor**

Acceder a un navegador para acceder al sitio web por el puerto *9090*.

La acción de publicar una entrada de acceso "externa" hacia el contenedor, se conoce como **routing mesh**

>**docker service create --name my-web --publish 8080:80 --replicas 2 nginx** [¿Qué hace esta ejecución?]

### Ejercicio 3 

Ahora a ver el update de imágenes, supongamos que se dispone de la aplicación Grafana con la version 5.0 y se desea desplegar en nuestro Cluster:

> docker service create --replicas 3 --name monitor **--update-delay 20s** grafana/grafana:5.0.0

donde:
–replicas: Es el número de tareas (task)
–name: Es el nombre del servicio.
–update-delay: Es el tiempo que transcurre entre la actualización de cada una de las tareas.
-grafana/grafana:5.0.0: Es la imagen que se va a emplear.

> docker service ls  && docker service ps $ID