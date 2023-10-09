# Practica 2: Instalación y configuracion de servidor DHCP Debian

## Indice

[Introduccion](#introduccion)

[Paso 1](#paso-1)

[Paso 2](#paso-2)

[Paso 3](#paso-3)

[Paso 1]()

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

  Despues cambiaremos el 

  ![Configuracion ip debian12](/1.png)

  ![Configuracion ip windows10 1](/21.png)

  ![Configuracion ip windows10 2](/18.png)

  ## Paso 3

  Despues de haber configurado todo lo de los pasos anteriores