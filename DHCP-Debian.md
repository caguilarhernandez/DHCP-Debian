# Practica 2: Instalación y configuracion de servidor DHCP Debian

## Indice

[Introduccion](#introduccion)

[Paso 1](#paso-1)

[Paso 2](#paso-2)

[Paso 3](#paso-3)

[Paso 4](#paso-4)

[Paso 5](#paso-5)

[Paso 6](#paso-6)

[Paso 7](#paso-7)

[Paso 8](#paso-8)

[Paso 9](#paso-9)

## Esquema

![Esquema](/Esquema.png)

## Introduccion

En esta practica vamos a hacer un tutorial de como instalar y configurar un servidor debian para que de ips automaticas a otros equipos que esten en la misma red.

## Paso 1

  Lo primero que hay que hacer es configurar las maquinas que vamos a utilizar posteriormente en esta practica. La primera es la maquina pfsense que tiene que tiene que tener dos tarjetas de red una en adaptador puente y otra en la red interna que vamos a usar que en este caso sera ASIR21.

  ![Configuracion red pfsense 1](/28.png) 

  ![Configuracion red pfsense 2](/27.png) 

  Despues configuro la tarjeta de red de la maqina debian para que sea de la misma red interna que el pfsense.

  ![Configuracion red debian12](/20.png) 

  Por ultimo configuro las dos maquinas windows10 que voy a usar en la misma red interna.

  ![Configuracion red windows10 1](/22.png)  

  ![Configuracion red windows10 2](/19.png)  

  ## Paso 2
  
  En este paso vamos a configurar las ips que deberian tener las maquinas. Empezamos por configurar la ip del pfsense que utilizaremos, que en mi caso sera el 192.168.1.1.

  ![Configuracion ip pfsense](/29.png) 

  Despues cambiaremos la configuración ip de la maquina debian12 a la ip 192.168.1.50 como está en el esquema facilitado anteriormente y con el dns del instituto 10.0.1.48.

  ![Configuracion ip debian12](/1.png)

  A continuación configuraremos las maquinas windows10 y para ello solo hace falta dejarlas en coger las configuraciones de forma automatica.

  ![Configuracion ip windows10 1](/21.png)

  ![Configuracion ip windows10 2](/18.png)

  ## Paso 3

  Despues de haber configurado los equipos de la misma forma que en los pasos anteriores, prodedemos a irnos a la maquina debian e instalar el servicio de servidor dhcp.
  Primero te pones en modo root.

~~~
su -
~~~

  Y despues pones el comando de instalacion.

~~~
apt install isc-dhcp-server
~~~

  ![Instalacion de servivio dhcp](/2.png)

  Despues de instalar el servicio de servidor dhcp miras con el siguinete comando la inforacion de donde estan ubicados los ficheros que vamos a necesitar para poder configurar el servidor dhcp de la maquina debian.

~~~
cat /etc/default/isc-dhcp-server
~~~

  ![Instalacion de servivio dhcp](/3.png)

  Editamos el fichero /etc/default/isc-dhcp-server para ponerle una interfaz en la direccion de ip v4 con el siguiente comando.

~~~
nano /etc/default/isc-dhcp-server
~~~

  ![Instalacion de servivio dhcp](/5.png)

  Comprobamos que se ha configurado la interfaz.

  ![Instalacion de servivio dhcp](/31.png)  

  ## Paso 4

  Despues de tener configurada la interfaz tendremos que copiar el fichero con el siguiente comando por si tenemos un fallo tener una copia.

~~~
cp /etc/default/isc-dhcp-server /etc/default/isc-dhcp-server.copia
~~~

  ![Instalacion de servivio dhcp](/4.png)  

  Luego nos moveremos al fichero /etc/dhcp y haremos un ls -alt para ver los ficheros y documentos que tenemos en ese fichero.

~~~
cd /etc/dhcp
~~~

  ![Instalacion de servivio dhcp](/6.png)  

  Luego haremos una copia de el documento que vamos a editar para configurar el servidor dhcp por si cometemos un error.

~~~
cp dhcpd.conf dhcpd.conf.copia
~~~

  ![Instalacion de servivio dhcp](/7.png)  

  ## Paso 5

  Ahora que ya hemos hecho ya la copia ya podemos empezar a configurar el servidor dhcp usando el siguiente comando. 

~~~
nano dhcp.conf
~~~

  Ahora ya dentro del documento de configuracion del servidor buscamos el apartado que es como en la siguiente imagen y nos ponemos a editarlo. Lo primero que tenemos que hacer sera poner la subnet que en mi caso sera la 192.168.1.0 y una mascara de 255.255.255.0. Despues pondremos el rango en el que tendremos que no poner la primera ip ya que es la del pfsense y tampoco pondremos la 50 ya que es la del propio servidor debian asique tendremos que partir el rango en dos partes una hasta la anterior a la ip 50 y la otra patte empezando desde la siguinete ip de la 50 hasta la 100. A continuacion pondremos el servidor dns, que en este caso sera el del instituto, y el nombre del dominio que en mi caso sera asir21.local. Luego pondre la ip del router, que al ser la del pfsense es la primera, seguido del tiempo de "alquiler" que le das por defecto, la maxima y la minima, que seran 8 horas, 24 horas y 1 hora, respectivamente.

  ![Instalacion de servivio dhcp](/8.png)

  Ahora buscaremos la plantilla del host fantasia en la que pondremos la mac, que es la ip fisica, de la maquina a la que queramos reservarle una ip en especifico. En este caso sera una maquina windows10 a la que le reservare la ip 60.

  ![Instalacion de servivio dhcp](/9.png)

  ## Paso 6

  Con la ayuda del comando :

~~~
systemctl status isc-dgcpd-server
~~~

  Podremos mirar si el servidor dhcp esta activo o no. Aqui podemos er que en este momento no esta activado.

  ![Instalacion de servivio dhcp](/10.png)

  Asique ahora nos ayudaremos de los comandos:

~~~
systemctl stop isc-dhcpd-server
~~~

~~~
systemctl start isc-dhcpd-server
~~~

  Que usaremos para reiniciar el servidor y ver si con esto podemos activar el servidor dhcp que estava inactivo.

  ![Instalacion de servivio dhcp](/11.png)

  Y aqui podemos observar que ya se me a activado el servidor dhcp.

  ![Instalacion de servivio dhcp](/12.png)

  Tambien podiamos haber usado el siguiente comando para reiniciar el servidor dhcp.

~~~
systemctl restart isc-dhcpd-server
~~~

  ![Instalacion de servivio dhcp](/13.png)

  Ahora miraremos los puertos para ver por cuales son los uertos por los que escucha con el siguiente comando.

~~~
ss -ltun
~~~

  ![Instalacion de servivio dhcp](/14.png)

  Y una vez vemos los puertos que escuchan volvemos a mirar el estado del servidor dhcp.

  ![Instalacion de servivio dhcp](/15.png)

  ## Paso 7

  Ahora vamos a entrar en el fichero /var/lib/dhcp/ y usaremos un ls para comprobar su contenido.

  ![Instalacion de servivio dhcp](/16.png)

  Ahora miraremos si la maquina windows10 ha cogido la ip del servidor dhcp que no tenia hecho un "alquiler" con el comando:

~~~
cat dhcpd.leases
~~~

  ![Instalacion de servivio dhcp](/17.png)

  Yo no tenia el windows10 encendido asique no lo cogio al principio hasta que al encenderlo y volver a poner el comando le hizo el lease.

  ![Instalacion de servivio dhcp](/23.png)

  Ahora miro en la otra maquina windows10 que tenia el "alquiler" de la ip 60 para ver si se lo ha dado bien con un comando:

~~~
ipconfig/all
~~~

  ![Instalacion de servivio dhcp](/25.png)

  ## Paso 8

  Ahora comprobare si las dos maquinas windows10 tienen conexion con el servisor dhcp y con internet haciendo ping a ambas.

  Le hago ping al servidor desde la maquina windows10 sin "alquiler".
  
  ![Instalacion de servivio dhcp](/24.png)

  Le hago ping al servidor desde la maquina windows10 con "alquiler".

  ![Instalacion de servivio dhcp](/26.png)

  Le hago ping a internet desde la maquina windows10 sin "alquiler".

  ![Instalacion de servivio dhcp](/32.png)

  Le hago ping a internet desde la maquina windows10 con "alquiler".

  ![Instalacion de servivio dhcp](/33.png)

  ## Paso 9

  Ahora miro los logs para ver los mensajes que han sido guardados en ellos con el siguiente comando.

~~~
journalctl -u isc-dhcp-server.services
~~~

![Instalacion de servivio dhcp](/30.png)

Como se puede ver a mi no me sale nada en los logs con respecto a los servicios de servidor dhcp. Sin embargo si me salen los logs si no lo hago especificamente a los servicios de servidor dhcp y lo hago de todas mis acciones en general.
