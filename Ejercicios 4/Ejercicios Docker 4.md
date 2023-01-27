# Ejercicios Docker 4
> Realizado por: Emilio Taibo

- Vamos a crear dos redes de ese tipo (BRIDGE) con los siguientes datos:

Red1:
- Nombre: red1
- Dirección de red: 172.28.0.0
- Máscara de red: 255.255.0.0
- Gateway: 172.28.0.1

Red2:
- Nombre: red2
- Es resto de los datos será proporcionados automáticamente por Docker
~~~
docker network create red1 --subnet 172.28.0.0/16 --gateway 172.28.0.1
docker network create red2

~~~
![](../Captura/CP4.1.png)

- Poner en ejecución un contenedor de la imagen ubuntu:20.04 que tenga como hostname
host1 , como IP 172.28.0.10 y que esté conectado a la red1. Lo llamaremos u1 .
~~~
docker run -it --name u1 --network red1 --hostname host1 --ip 172.28.0.10 ubuntu:20.04 
~~~
![](../Captura/CP4.2.png)
-  Entrar en ese contenedor e instalar la aplicación ping ( apt update && apt install
inetutils-ping ).
~~~
    docker start u1
    docker excec -it u1 bash
    apt update
    apt install inetutils-ping
~~~
![](../Captura/CP4.3.png)
-  Poner en ejecución un contenedor de la imagen ubuntu:20.04 que tenga como hostname
host2 y que esté conectado a la red2. En este caso será docker el que le de una IP correspondiente
a esa red. Lo llamaremos u2 .
~~~
docker run -it --name u2 --network red2 --hostname host2 ubuntu:20.04
~~~
![](../Captura/CP4.4.png)
- Entrar en ese contenedor e instalar la aplicación ping ( apt update && apt install
inetutils-ping ).
~~~
    docker start u2
    docker excec -it u2 bash
    apt update
    apt install inetutils-ping
~~~
![](../Captura/CP4.5.png)

- Contenedor u1
![](../Captura/CP4.6.png)
![](../Captura/CP4.7.png)
- Contenedor u2
![](../Captura/CP4.8.png)
![](../Captura/CP4.9.png)
- Pantallazo donde desde cualquiera de los dos contenedores se pueda ver que no podemos hacer ping al
otro ni por ip ni por nombre
![](../Captura/CP4.10.png)
- Pantallazo donde se pueda comprobar que si conectamos el contenedor u1 a la red2 (con docker
network connect ), desde el contenedor u1, tenemos acceso al contenedor u2 mediante ping, tanto
por nombre como por ip.
![](../Captura/CP4.11.png)

