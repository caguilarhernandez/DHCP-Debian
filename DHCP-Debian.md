# Practica 2: Instalación y configuracion de servidor DHCP Debian

## Indice

[Paso 1](#paso-1)

[Paso 2](#paso-2)

[Paso 1]()

[Paso 1]()

[Paso 1]()

## Esquema

![Esquema](/Esquema.png)

## Paso 1

  Lo primero que hay que hacer es configurar las maquinas que vamos a utilizar posteriormente en esta practica. La primera es la maquina pfsense que tiene que tiene que tener dos tarjetas de red una en adaptador puente y otra en la red interna que vamos a usar que en este caso sera ASIR21 y configuraremos su ip lan a la red 192.168.1.1 con la opcion 2 que te da el pfsense.

  ![Configuracion red pfsense 1](/28.png) 

  ![Configuracion red pfsense 2](/27.png) 

  ![Configuracion ip pfsense](/29.png) 

  Despues configuro la tarjeta de red de la maqina debian para que sea de la misma red interna que el pfsense y le doy a el servidor debian12 una ip fija que en este caso sera la 192.168.1.50.

  ![Configuracion red debian12](/20.png) 

  ![Configuracion ip debian12](/1.png) 

  Por ultimo configuro las dos maquinas windows10 que voy a usar, siendo una para hacer una reserva y la otra para que le una ip aleatoria.

  ![Configuracion red windows10 1](/22.png) 

  ![Configuracion ip windows10 1](/21.png) 

  ![Configuracion red windows10 2](/19.png) 

  ![Configuracion ip windows10 2](/18.png) 

  ## Paso 2

  