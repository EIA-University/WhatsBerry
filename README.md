# WhatsBerry

En la actualidad, WhatsApp es una herramienta de comunicacion básica para las personas. Desde empresarios hasta jovenes estudiantes lo utilizan, para comunicacion simple hasta compartir documentos y demás archivos que se necesitan hacer llegar a las personas de forma rápida. En las ultimas actualizaciones se ha logrado mejorar la seguridad con la que compartimos información con nuestros contactos pero aún falta mucho por mejorar. Es por ello que se plantea un sistema en el cual podemos acceder al sistema, conocer las librerías que utiliza y comunicarnos desde la consola de nuestro pc.

Para este proyecto se deben seguir una serie de pasos y tener conocimientos previos de python y raspberry

Elementos Necesarios:

-Raspberry Pi 3
-SD card de 8gb o mas
-Sim card sin whatsapp registrado

Pasos a seguir:
1.Antes de entrar a trabajar con las librerias de Yowsupp debemos preparar el entorno de trabajo instalando python y buscando las          librerias necesarias,para lo cual ejecutamos:

$ sudo apt-get install git python-dev libncurses5-dev

2.Descargamos las librerias de Yowsupp, para esto ejecutamos el siguiente comando en la consola:

$ git clone git://github.com/tgalal/yowsup.git

3.Ahora vamos a la carpeta donde lo instalamos,el cual sera el directorio donde se ejecuto el comando anterior,y dentro de esta carpeta ejecutamos el comando para instalar el setup:

$cd Yowsupp

$sudo python setup.py install

4.Ahora debemos registrar un telefono con el cual trabajaremos (El de la sim),para esto creamos un archivo llamado mydetails y ponemos el numero de identificacion de cada pais,en este caso 57 para colombia,y luego el telefono de la sim con la prepocision del numero de identificacion:

$ nano mydetails

cc=57

phone=573002354706

5.Despues de Guardar el archivo del paso anterior,ahora le pedimos un codigo de confirmacion a whatsapp

$ python yowsup-cli registration --config mydetails --requestcode sms

Despues de unos momentos recibiras un sms al celular de la sim que habias ingresado,recibiras un codgigo de 6 digitos xxx-xxx

6.registramos nuestro numero ingresando el siguiente comando (reemplazamos las xxx-xxx por el codgio que llego al celular):

$ python yowsup-cli registration --config mydetails --register xxx-xxx

Se recibira un codigo como el siguiente:

status: ok
kind: free
pw: jK0zdPJ9zz0BBC3CwmnLqmxuhBk=
price: 0.89
price_expiration: 1434674993
currency: EUR
cost: 0.89
expiration: 1463544490
login: 448375972334
type: new

7.Esto demostrara que se hizo el registro correctamente, el dato importante de este mensaje recibido es el PW,esta contraseña larga que incluyendo el = del final

8.Ahora vamos a mydetails y añadimos una linea que se llame password=jK0zdPJ9zz0BBC3CwmnLqmxuhBk= y le adjuntamos el pw del mensaje recibido,el archivo deberia quedar asi:

cc=57
phone=573002354706
password=jK0zdPJ9zz0M8G3CwmnLqmxuhBk=

9.Ahora descargamos el archivo layers de este repositorio y lo reemplazamos en yowsup-Master/yowsup/demos/echoclient 

10. ejecutamos los el archivo con $ yowsup-cli demos --echo --config mydetails



