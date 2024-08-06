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

 ##  

