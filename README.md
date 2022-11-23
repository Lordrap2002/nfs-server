# nfs-server
Comandos del proyecto:
En el host:

`apt update`

`apt install sudo`

`sudo apt install nfs-kernel-server -y`

`sudo apt install rpcbind`

`sudo service rpcbind restart`

`sudo service nfs-kernel-server start`

`sudo service nfs-kernel-server restart`

`sudo service docker start`

`sudo service rpcbind restart`

`docker run                                           \
  -v /home/prueba:/data  \
  -v /etc/exports:/etc/exports:ro        \
  --name cont0 \
  --cap-add SYS_ADMIN                                 \
  -p 2049:2049   -p 2049:2049/udp   \
  -p 32765:32765 -p 32765:32765/udp \
  -p 32767:32767 -p 32767:32767/udp \
  erichough/nfs-server`
  
SALIR DEL CONTENEDOR

`sudo docker start cont0`

`sudo docker exec -it cont0 /bin/bash`

`chown nobody:nogroup /data`

`chmod 777 /data`


En el cliente:

`docker run -di                                           \
  --name cont1 \
  --cap-add SYS_ADMIN                                 \
  ubuntu:20.04`
  
`docker exec -it cont1 /bin/bash`

`apt update -y`

`apt install nfs-kernel-server -y`

`apt install nfs-common -y`

`service rpcbind restart`

`service nfs-common start`

`apt-get install systemd -y`

`systemctl mask rpcbind`

``apt-get install vim -y`

`mkdir /home/datos1`

`mount -o rw,vers=3 172.17.0.2:/data /home/datos1`

`df -h`

`touch file1.txt`

`mkdir dir1`

`umount /home/datos1`

Para el volumen:

`sudo apt install nfs-common`

`docker volume create --driver local \
  --opt type=nfs \
  --opt o=addr=172.17.0.2,rw \
  --opt device=:/data \
  nfs-volume`
  
`docker volume ls`

`docker volume inspect nfs-volume`

`docker run -d -it \
  --name cont3 \
  --mount source=nfs-volume,target=/home \
  ubuntu`
  
`docker inspect cont3`

`docker exec -it cont3 /bin/bash`

`ls home`
