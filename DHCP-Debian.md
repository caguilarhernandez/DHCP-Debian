# Practica 2: Instalación y configuracion de servidor DHCP Debian

## Indice

[Introduccion](#introduccion)

[Paso 1](#paso-1)

[Paso 2](#paso-2)

[Paso 3](#paso-3)

[Paso 4](#paso-4)

[Paso 1]()

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

  ![Instalacion de servivio dhcp](/32.png)

  ## Paso 4

  Despues de tener configurada la interfaz tendremos que cambiarnos a 

  ![Instalacion de servivio dhcp](/4.png)  

  ![Instalacion de servivio dhcp](/5.png)  