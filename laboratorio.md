# Documentación del primer laboratorio

## Imagén de ubuntu
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
9c704ecd0c69: Pull complete 
Digest: sha256:2e863c44b718727c860746568e1d54afd13b2fa71b160f5cd9058fc436217b30
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest

## Imagén de python versión especifica
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker pull python:3.9
3.9: Pulling from library/python
ca4e5d672725: Pull complete 
30b93c12a9c9: Pull complete 
10d643a5fa82: Pull complete 
d6dc1019d793: Pull complete 
c387064957b7: Pull complete 
26766ebde481: Pull complete 
8a42d17fd0e2: Pull complete 
79eda865cc8a: Pull complete 
Digest: sha256:fea84f3a3b72c41efe7fc3b07ae209c6856b852b942c05fa88b747b74f70e711
Status: Downloaded newer image for python:3.9
docker.io/library/python:3.9

## Ejecución iterativa de ubuntu
root@c3740fce6aa6:/# 

## Descarga y ejecución en segundo plano mapeada de servidor web de Apache
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker pull httpd
Using default tag: latest
latest: Pulling from library/httpd
efc2b5ad9eec: Already exists 
fce1785eb819: Pull complete 
4f4fb700ef54: Pull complete 
f214daa0692f: Pull complete 
05383fd8b2b3: Pull complete 
88ad12232aa1: Pull complete 
Digest: sha256:932ac36fabe1d2103ed3edbe66224ed2afe0041b317bcdb6f5d9be63594f0030
Status: Downloaded newer image for httpd:latest
docker.io/library/httpd:latest
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker run -d -p 8000:80 httpd
537b0a82a5d3e4f2ce19ddf89d07ad6f912548189bd06a7ca476273e3df49eac

## Eliminación del contendor de ubuntu
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                     PORTS                                   NAMES
537b0a82a5d3   httpd     "httpd-foreground"       3 minutes ago    Up 3 minutes               0.0.0.0:8000->80/tcp, :::8000->80/tcp   festive_heisenberg
c3740fce6aa6   ubuntu    "bash"                   14 minutes ago   Exited (0) 7 minutes ago                                           brave_lamarr
8aa705a14c0c   nginx     "/docker-entrypoint.…"   16 minutes ago   Up 16 minutes              0.0.0.0:8080->80/tcp, :::8080->80/tcp   wizardly_rosalind
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker rm c3740fce6aa6
c3740fce6aa6
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
537b0a82a5d3   httpd     "httpd-foreground"       5 minutes ago    Up 4 minutes    0.0.0.0:8000->80/tcp, :::8000->80/tcp   festive_heisenberg
8aa705a14c0c   nginx     "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes   0.0.0.0:8080->80/tcp, :::8080->80/tcp   wizardly_rosalind

## Eliminación de todos los contendores detenidos 
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker container prune -f
Total reclaimed space: 0B

# Documentación del segundo laboratorio

## Crear, construir un dockerfile básico y actualizar paquetes: ejercicio 1 y 2
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker build -t ubuntu-updated:latest .
[+] Building 8.6s (6/6) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 96B                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                             0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 2B                                                                                                              0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                                               0.1s
 => [2/2] RUN apt-get update && apt-get upgrade -y                                                                                           7.2s
 => exporting to image                                                                                                                       0.7s 
 => => exporting layers                                                                                                                      0.6s 
 => => writing image sha256:48505686bd00a6e2d63b342bb780bd7a0f8a920a3c096d5c29c2f29310b9712d                                                 0.0s 
 => => naming to docker.io/library/ubuntu-updated:latest   

 ## Dockerfile para instalar nginx en ubuntu
 +] Building 13.1s (6/6) FINISHED                                                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.0s
 => => transferring dockerfile: 137B                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                             0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 2B                                                                                                              0.0s
 => CACHED [1/2] FROM docker.io/library/ubuntu:latest                                                                                        0.0s
 => [2/2] RUN apt-get update && apt-get install -y nginx                                                                                    11.9s
 => exporting to image                                                                                                                       0.7s 
 => => exporting layers                                                                                                                      0.5s 
 => => writing image sha256:cfdd831568e6488571caf751eed03fcb5c9e83700f56be57f4e7091fbb458006                                                 0.0s 
 => => naming to docker.io/library/ubuntu-updated:latest  

 ## Construcción y ejecucion de la imagén de nginx

 ### Construcción
 @SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker build -t my-nginx:latest .
[+] Building 0.5s (6/6) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 137B                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                             0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 2B                                                                                                              0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                                               0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y nginx                                                                              0.0s
 => exporting to image                                                                                                                       0.1s
 => => exporting layers                                                                                                                      0.0s
 => => writing image sha256:cfdd831568e6488571caf751eed03fcb5c9e83700f56be57f4e7091fbb458006                                                 0.0s
 => => naming to docker.io/library/my-nginx:latest  

 ### Ejecución
 @SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker run -d -p 80:80 my-nginx:latest
558082a0e8ec6b07523be5fb34467c7a7fd5f6761fd6d175d0a55288f2d8bd06

## Modificación del dockerfile para exponer el puerto 80
@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker build -t my-nginx:latest .
[+] Building 0.6s (6/6) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 147B                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                             0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 2B                                                                                                              0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                                               0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y nginx                                                                              0.0s
 => exporting to image                                                                                                                       0.1s
 => => exporting layers                                                                                                                      0.0s
 => => writing image sha256:85eb6770455fac42ade70a4eb01835823fdabe9eb010cf3a8998895845888a87                                                 0.0s
 => => naming to docker.io/library/my-nginx:latest   

 ## Copiar un archivo html local a una imagén de nginx
 @SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker build -t my-nginx:latest .
[+] Building 2.4s (7/7) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 93B                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                                              0.0s
 => [internal] load .dockerignore                                                                                                            0.0s
 => => transferring context: 2B                                                                                                              0.0s
 => [internal] load build context                                                                                                            0.4s
 => => transferring context: 256B                                                                                                            0.0s
 => [1/2] FROM docker.io/library/nginx:latest                                                                                                0.8s
 => [2/2] COPY index.html /usr/share/nginx/html/                                                                                             0.2s
 => exporting to image                                                                                                                       0.7s
 => => exporting layers                                                                                                                      0.5s
 => => writing image sha256:81a5780446db5f61954a7ec6a43450d0d80ab23442f79cc2746bfa121fd32b0c                                                 0.0s
 => => naming to docker.io/library/my-nginx:latest  

 ## Usar WORKDIR y copiar un archivo

@SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker build -t ubuntu-updated:latest .
[+] Building 1.6s (8/8) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 86B                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                             0.0s
 => [internal] load .dockerignore                                                                                                            0.0s
 => => transferring context: 2B                                                                                                              0.0s
 => [1/3] FROM docker.io/library/ubuntu:latest                                                                                               0.0s
 => [internal] load build context                                                                                                            0.1s
 => => transferring context: 31B                                                                                                             0.0s
 => CACHED [2/3] WORKDIR /app                                                                                                                0.0s
 => [3/3] COPY myfile.txt .                                                                                                                  0.3s
 => exporting to image                                                                                                                       0.8s
 => => exporting layers                                                                                                                      0.7s
 => => writing image sha256:731f5cbc875db64d295a4482fff0799cd1d6ee950f55459b3e0a3d49d7b74d4e                                                 0.0s
 => => naming to docker.io/library/ubuntu-updated:latest 


## Ejecutar un script Python al iniciar el contenedor
 @SamuelCG040921 ➜ /workspaces/labs-docker-dev (main) $ docker build -t python:3.9 . 
[+] Building 3.8s (8/8) FINISHED                                                                                                   docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 110B                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/python:3.9                                                                                0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 2B                                                                                                              0.0s
 => [1/3] FROM docker.io/library/python:3.9                                                                                                  0.0s
 => [internal] load build context                                                                                                            0.1s
 => => transferring context: 30B                                                                                                             0.0s
 => CACHED [2/3] WORKDIR /app                                                                                                                0.0s
 => [3/3] COPY script.py .                                                                                                                   0.3s
 => exporting to image                                                                                                                       2.9s
 => => exporting layers                                                                                                                      2.7s
 => => writing image sha256:3c1b0ddfbc40196f7c0d34cc48a62758686431d33d94d1c3875dd75ade1c3baf                                                 0.0s
 => => naming to docker.io/library/python:3.9     