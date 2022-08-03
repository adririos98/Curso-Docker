```shell
[root@anacoluto-win ~]# docker run -dit ubuntu:22.04
ff4658a0d2d1847879aad9cb7c1cfbdc3c03efe15cebe54787e5d09da9cc0824

[root@anacoluto-win ~]# docker ps
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS          PORTS     NAMES
ff4658a0d2d1   ubuntu:22.04   "bash"    36 seconds ago   Up 34 seconds             laughing_rubin

[root@anacoluto-win ~]# docker exec -it ff4658a0d2d1 bash

root@ff4658a0d2d1:/# cd /tmp/

root@ff4658a0d2d1:/tmp# touch prueba.txt

root@ff4658a0d2d1:/tmp# ls -lrta
total 0
drwxr-xr-x. 1 root root 17 Aug  3 10:55 ..
-rw-r--r--. 1 root root  0 Aug  3 10:57 prueba.txt
drwxrwxrwt. 1 root root 24 Aug  3 10:57 .

root@ff4658a0d2d1:/tmp# exit
exit

[root@anacoluto-win ~]# docker ps
CONTAINER ID   IMAGE          COMMAND   CREATED         STATUS         PORTS     NAMES
ff4658a0d2d1   ubuntu:22.04   "bash"    2 minutes ago   Up 2 minutes             laughing_rubin

[root@anacoluto-win ~]# docker commit ff4658a0d2d1
sha256:7a761719b535773394065d5b708cb4e074d278c7bcf258129ccbf25a3f1360a7

[root@anacoluto-win ~]# docker image ls
REPOSITORY                                               TAG             IMAGE ID       CREATED          SIZE
<none>                                                   <none>          7a761719b535   12 seconds ago   77.8MB

[root@anacoluto-win ~]# docker tag 7a761719b535 prueba-curso:1.0
[root@anacoluto-win ~]# docker image ls
REPOSITORY                                               TAG             IMAGE ID       CREATED              SIZE
prueba-curso                                             1.0             7a761719b535   About a minute ago   77.8MB
```