 1.
Lo primero que tenemos que hacer es crear un contenedor con docker run -dit --name examen ubuntu y una vez creado podemos abrir una terminal con docker exec -it u1 bash

2.
-dit para poder crear un contenedor en modo interactivo

3.
Esto se configura en el contenedor docker-compose.yml
services:
  contenedor1:
    container_name: contenedor1
    image: ubuntu/bind9
    plataform. linux/amd64
4.
Abria que añadirle el apratado ipv4_address

5.
Con este comando podemos obtener las ips de los contenedores
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'bono

6.
El apartado ports nos permite definir por cual puerto queremos que se comunique el servicio. Es muy importante asegurarse de que el puerto que estamos poniendo en ports no este siendo utilizado por otro servicio

7.
A) Define un alias para el nombre canónico.
B) Suministrar un nombre alternativo relacionado con un servicio en el equipo. Muy util cuando hay varios servicios en el mismo equipo

8.

9.

Para este ejercicio voy a utilicar un contenedor ya montado cambiando el nombre del contenedor principal y del cliente y las ips, todo esto en el archivo docker-compose.yml

container_name: tendaelectronica
ipv4_address: 172.16.0.1

El siguiente archivo  que hay que configurar es el named.conf.local:

zone "tendaelectronica.int" {
    	type master;
    	file "/var/lib/bind/db.tendaelectronica.int";
    	allow-query {
            	any;
            	};
    	};


Ahora voy a la carpeta zona y creo el archivo db.tendaelectronica.int.
owncloud sexa un CNAME de www:

www in CNAME owncloud 172.16.0.7

un rexistro de texto có contido "1234ASDF:

texto in TXT 1234ASDF

Continuo con el apartado de configurar una red la cual configurare por terminal:

$ docker network create tenda_subnet
$ docker network create \
  --driver=bridge \
  --subnet=172.16.0.1/16 \
  --ip-range=172.16.5.0/24 \
  --gateway=172.16.5.254 \
  tenda_subnet

  Utilizo el comando docker compose up para iniciar el contenedor

  Por ultimo queda la instalacionde dig con el cual vamos a poder realizar consultas y para poder instalarlo voy a utilizar los siguientes comandos:

$ docker exec -it nombre_contenedor bash
$ apt update
$ apt install -y dnsuit

Para comprobar el funcionamiento de dig utilizare este comando:
$ dig @172.16.0.1 ns.tendaelectronica.int

desgraciadamente no puedo llegar hasta este paso ya que en docker compose up me salta este error.

[+] Running 0/0
 ⠋ Container tendaelectronica_bin9  C...                               	0.0s
 ⠋ Container cliente3           	Creating                           	0.0s
Error response from daemon: invalid config for network 7976d3343f930a351acaf7d9db0f2c5a7eeb3f4ba280a8dea095c2f8deb3cb03: invalid endpoint settings:
user specified IP address is supported only when connecting to networks with user configured subnets








