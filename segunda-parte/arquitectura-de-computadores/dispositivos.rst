20. Dispositivos
================

Cuando se enfrentan a una computadora por primera vez seguramente lo primero que verán será una pantalla y un teclado, de hecho para mucha gente 
esa es la imagen del computador, aunque eso está cambiando, con la introducción de los tablets, por ejemplo, el computador queda reducido a una pantalla
interactiva en el imaginario de muchas personas. La CPU, el verdadero motor del computador está escondido, es apenas un minúsculo chip de silicio.

En nuestro diagrama dibujamos dos bloques en la parte inferior, INPUT y OUTPUT los llamamos. Esos bloques son abstracciones para designar
a todas las piezas que permiten conectar a la cpu con el mundo externo. Esos bloques no corresponden a los **dispositivos externos**, como la pantalla, 
el teclado, el mouse, micrófonos, parlantes, etc. Lo que representan esos bloques son las interfaces que permiten conectarse con esos dispositivos.

.. figure:: /_static/programando-cpu1.png
   :scale: 100 %
   :alt: Diagrama de Bloques de nuestra máquina virtual
   :align: center
   
Por ejemplo, cuando escuchan un MP3 en un aparato reproductor de este tipo de archivos, lo que tienen es una cpu que interpreta los bits
almacenados en los archivos .mp3 y los decodifica entregando una serie de instrucciones a un dispositivo que transforma esos bits en audio que
se emite a través de un audífono.


¿Cómo controla la CPU a los distintos dispositivos?
---------------------------------------------------

En nuestra CPU simulada teníamos una instrucción que llamamos ``IMPR``. En una CPU real una instrucción como esta no existe.
En una CPU real hay comandos que permiten instruir a los módulos INPUT/OUTPUT y son estos los que se encargan de traducir estos comandos
en acciones sobre un dispositivo.

Ahora bien, los módulos INPUT/OUTPUT deben ser capaz de controlar una gama amplia y desconocida de dispositivos. Seguramente cuando han 
comprado un nuevo dispositivo para su computador han tenido que instalar una pieza de software adicional, normalmente 
conocida como controlador o driver. Esa pieza de software corresponden a instrucciones que son interpretadas por estos módulos de INPUT y OUTPUT
para poder dar instrucciones al nuevo dispositivo. Lo que hace el controlador es aumentar las capacidades del computador, amplía su rango de acción.

La CPU no aumenta su vocabulario de comandos, porque está fijado desde fábrica, son los otros módulos auxiliares de la CPU los que se encargan
de ayudar a que la cpu pueda operar estos nuevos dispositivos.

Supongamos que nuestra CPU sólo tiene la instrucción OUT, que recibe dos parámetros: id y mem. El parámetro id identifica al dispositivo, por ejemplo, 
1 será la pantalla, 2 una impresora, 3 el parlante. El parámetro mem indica una dirección de memoria donde se encuentra un mensaje. Entonces si tenemos
la instrucción: ``OUT 2, 4452`` escribirá en la impresora el texto que se encuentra en la dirección de memoria 4452. 
Por otro lado, la instrucción ``OUT 1, 4452`` escribirá en pantalla el mismo texto, y finalmente ``OUT 3, 4452`` "dirá el texto" por el parlante del computador.
La CPU solo conoce la instrucción OUT, el cómo se materializa es responsabilidad del módulo OUTPUT, el que a su vez usará los controladores
respectivos de cada dispositivo para lograr este cometido.

Lo mismo pasa con los dispositivos que son usados para capturar datos, como el teclado o el mouse. Cada uno tiene un controlador que es manejado
por los módulos de INPUT. En este caso los datos no necesariamente son entregados a la CPU para que los procese. Normalmente los datos son almacenados
en memoria directamente y la CPU los rescata cuando los necesita.

Como pueden ver, el computador, es una máquina bastante compleja, pero muy flexible y poderosa. Esa es la razón de su éxito y su ubicuidad.
Hay computadores en todas partes, en nuestros televisores, automóviles, teléfonos hasta en el refrigerador, y en un futuro tendremos computadores
en nuestra propia ropa. 

Con esto concluimos nuestro breve barniz sobre la arquitectura de computadores. Ya tenemos algo de conocimiento básico que nos permite enfrentar
un desafío más entretenido: la programación de juegos.

Ejercicios
----------

    1. Modifica el código de nuestra máquina virtual eliminando las instrucciones IMPR y LEER por las instrucciones IN y OUT, de modo que
	 estas reciban el número de dispositivo (1: pantalla, 2: teclado, 3: impresora, 4: audio).
	 
    2. Crea las funciones IN y OUT que implementen las instrucciones del ejercicio anterior, para que a su vez invoquen a distintas funciones 
	 dependiendo del dispositivo usado.
	 


