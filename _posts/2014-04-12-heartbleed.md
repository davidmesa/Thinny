---
layout: post
title: "Heartbleed"
quote: "Internet cae a los pies de un error ridículo"
image: /media/2014-04-12-heartbleed/cover.jpg
video: false
comments: true
---
Es el primer bug de seguridad en tener su propio sitio web y logo, simplemente es impresionante ver como una vulnerabilidad se convirtió en una súper estrella en internet, afectando a mas del 66% de los sitios y seguramente entre esos están los que utilizan diariamente. Heartbleed es excepcional desde cualquier punto que se vea, su sencillez, su duración en versiones estables de OpenSSL y sus implicaciones con el programa espía de la NSA.

Para comenzar es importante recalcar que Heartbleed no es un virus, es un error en implementación algo ridículo, lo cual demuestra que el software siempre va ser vulnerable gracias a la imperfección o malas intenciones de los humanos. No quiero entrar a discutir teorías conspiraciones, pero a mi parecer este bug parece más un backdoor estúpidamente implementado que un error de un programador experimentado.  Volviendo a los hechos, fue introducido en diciembre del 2011 y el parche fue entregado en abril 7 del 2014, dando un espacio de tiempo de más de 2 años en los cuales nos han podido afectar.


## ¿Cómo funciona?

Seguramente han visto un https en la parte superior del explorador, lo cual quiere decir que la información que se transmite con el sitio web esta siendo encriptada, seguramente con OpenSSL, para que terceros no la puedan interceptar. OpenSSL, el cual fue afectado, implementa una extensión conocida como Heartbeat, la cual permite mantener una conexión entre el cliente y el servidor corriendo, aunque no se haya transmitido información en algún tiempo, enviando un “latido” para demostrar que aun sigue vivo el proceso en el otro extremo, ya que es costoso volver a crear un canal de comunicación.


<br>

{% include image.html url="/media/2014-04-12-heartbleed/cliente-servidor.jpg" width="100%" %}


El latido contiene dos fragmentes importantes para el entendimiento de este bug, el contenido del mensaje (payload) y el tamaño de dicho mensaje. Cuando el servidor recibe este heartbeat del cliente, devuelve exactamente el mismo mensaje con algo de relleno. El problema radica en que el latido puede ser construido de cualquier manera que el atacante se le ocurra. Por lo tanto puede escribir un Byte en el payload y decir que el mensaje contiene 65KB de información. Consecuentemente el servidor va a extraer los 65KB que el mensaje dice contener, de su memora y los devuelve. Lo que implica que el mensaje de retorno no solo contiene el payload del latido original, sino que todo lo que le seguía en memoria, lo cual podría ser información confidencial.

## ¿Cómo Protegernos?

No es posible conocer las implicaciones de este error, ya que los latidos no dejan rastro en el servidor, por lo tanto la fuga de información puede ser extremadamente alta, o casi nula, pero es mejor prevenir que lamentar. Por lo tanto, los pasos a seguir son simples. Primero asegúrese que las paginas que utiliza ya hayan instalado el parche en sus servidores, y DESPUES de que el sitio ya no sea vulnerable es muy recomendable cambiar sus credenciales e información sensible.


<br>

**David Mesa**






