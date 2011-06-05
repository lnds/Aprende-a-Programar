.. highlight:: python
    :linenothreshold: 2

9. Funciones
============

En el capítulo anterior aprendimos a construir un clon del ambiente IDLE de Python. La verdad es que el programa resultante tiene sus limitaciones, pues no permite ejecutar todas las instrucciones del lenguaje como lo hace IDLE, pero funciona bastante bien como calculadora. Vamos a expandir ese programa para darle más funcionalidades de calculadora.

Construyendo nuestra propia calculadora
---------------------------------------

El ejercicio 4 de la lección anterior dice así: *Modifica el programa para que incorpore las variables “pre definidas” pi = 3.1415 y e = 2.71828 de modo que puedan ser usada en las expresiones*.

Ahora intentaremos resolver este ejercicio modificando el código de nuestro clon de IDLE. Una cosa que podemos hacer es declarar las variables ``pi`` y ``e`` antes de empezar el ciclo infinito, eso debería resultar: 


  .. code-block:: python

     # declaramos las variables "pre definidas"  
     pi = 3.1415  
     e = 2.71828  

     while True: # loop infinito    
  
        	# 1. Necesitamos leer la <strong>instrucción</strong> que el usuario quiere ejecutar, y la guardaremos en un string  
        	instrucción = input("-->")    
  
        	# 2. Evaluaremos el string ingresado en el paso 1. usando la función eval() vamos a almacenar el  resultado  
        	resultado = eval(instrucción)    
  
        	# 3. Mostraremos en pantalla el resultado obtenido en el paso 2.  
        	print(resultado)  

Vamos a aprovechar de renombrar nuestro programa y lo llamaremos calculadora-1.py, este es el resultado de la ejecución en mi pc: 

.. figure:: /_static/calculadora-1.png
   :scale: 80 %
   :alt: calculadora1.py
   :align: center

Obteniendo ayuda de python
**************************

En la construcción de nuestra primera calculadora hemos usado tres funciones: ``input()``, ``print()`` y ``eval()``. Python tiene incorporada una función especialmente útil en el ambiente interactivo de IDLE, se trata de ``help()``.

Veamos que ocurre cuando invocamos help en el IDLE, usando el nombre de cada una de estas funciones como argumento:

.. figure:: /_static/help-python.png
   :scale: 80 %
   :alt: ayuda en python
   :align: center

Lo primero que observamos es que está todo el texto en inglés, no puedes dedicarte a la programación si no pules tu inglés,debes aprender inglés, es urgente,  english is required, an that’s is non negotiable.

Lo segundo, es la forma en que son presentadas las explicaciones de cada función, junto al nombre de cada función aparace cómo se le entregan los argumentos a cada función. Cuando los argumentos aparecen entre paréntesis cuadrados ([ y ]) significa que son argumentos opcionales. Por ejemplo, la función input recibe opcionalmente un argumento prompt.

Lo tercero, y que es bastante interesante, es que podemos ejecutar la función `help()` en nuestro programa calculadora-1.py, cortesía de la función `eval()`, anda pruébalo.

Nuestras propia funciones
*************************

Las funciones ``input()``, ``eval()`` y ``print()`` están pre definidas en python. Nosotros podemos escribir nuestras propias funciones y es lo que vamos a hacer ahora.

Si recuerdan mi primer programa permite convertir temperaturas expresadas en grados Fahrenheit a la escala Celsius. Esas son dos funciones interesantes que podemos incorporar a nuestra calculadora. Una función que convierta de grados fahrenheit a celsius y otra que haga la operación inversa.

¿Cómo nombrar a estas funciones?

Hay varias opciones: ``convertir_fahrenheit_a_celsius()``, ``fahrenheit_a_celsius()``, ``conv_fahr_a_cel()``, ``f_a_c()``, ``f2c()``, etc.Elegir el nombre de una función es una tarea importante, debemos favorecer dos aspectos: concisión y claridad. La primera opción es bastante clara, pero consideremos que no sería muy práctica en una calculadora interactiva, con ese nombre sería muy fácil que el usuario se equivocara, de hecho el nombre Fahrenheit ya es bastante dificil de escribir.

He decidido usar el nombre ``fahrcel()`` para la función que convierte desde grados fahrenheit a celsius y ``celfahr()`` para el nombre de la función inversa.

La siguiente es la definición de ambas funciones en python:

.. code-block:: python

   def fahrcel(grados):  
       """Recibe un valor expresado en grados Fahrenheit 
          y lo retorna expresado en grados Celsius"""  
       return (grados - 32) / 1.8  
  
   def celfahr(grados):  
       """Recibe un valor expresado en grados Celsius y 
          lo retorna expresado en grados Fahrenheit"""  
       return grados*1.8 + 32  

Una función en python se introduce, o **declara**, usando la palabra clave ``def``, luego colocamos el nombre de la función y sus argumentos entre paréntesis. En este caso nuestras dos funciones sólo tienen un argumento (grados).

Las lineas que siguen corresponde al cuerpo de la función, que son la secuencia de instrucciones que serán ejecutadas cada vez que esta función sea **invocada**.

Notarás que el cuerpo de la función se encuentra debidamente identado, es decir, tiene una sangía de 4 espacios antes del texto. Esto es muy importante en python, todo el resto del bloque de instrucciones que pertenezcan a la función deben mantener esta sangría o identación.

La primera instrucción de cada función es un string encerrado entre comillas triples (“”"), esto permite escribir un string que puede extenderse por varias lineas. Este primer string es interpretado por python como la documentación de la función, y es usado por la función help() para obtener la descripción de la función.

Estas son funciones bastante simples, que realizan un cálculo aritmético con su argumento. Toda función que retorna un resultado debe contener la instrucción return. Al colocar return expresión hacemos que la función termine y retorne un resultado a quien la haya invocado.
Probemos escribiendo estas funciones en IDLE, acá va un pantallazo de una sesión de pruebas:

.. figure:: /_static/probando-funciones.png
   :scale: 80 %
   :alt: probando funciones
   :align: center

Fíjense en como la función ``help()`` reconoce nuestras funciones y despliega la documentación que hemos escrito de cada una al principio de la declaración.

Calculadora versión 2
*********************

Vamos a renombrar nuestro anterior programa calculadora-1.py como calculadora-2.py y vamos incorporar estas funciones al inicio de nuestro programa:

.. code-block:: python

   # declaramos las variables "pre definidas"  
   # calculadora-2.py  
  
   # define 2 funciones para convertir temperaturas:  
  
   def fahrcel(grados):  
      """Recibe un valor expresado en grados Fahrenheit 
         y lo retorna expresado en grados Celsius"""  
      return (grados - 32) / 1.8  
  
   def celfahr(grados):  
      """Recibe un valor expresado en grados Celsius y 
      lo retorna expresado en grados Fahrenheit"""  
      return grados*1.8 + 32  
  
   # define 2 variables predefinidas  
  
   pi = 3.1415  
   e = 2.71828  
  
   # registramos la versión de este programa  
   version = 2  
  
   print ("Calculadora versión:", version)  
  
   while True: # loop infinito    
  
        # 1. Necesitamos leer la <strong>instrucción</strong> que el usuario quiere ejecutar, y la guardaremos en un string  
        instrucción = input("-->")    
  
        # 2. Evaluaremos el string ingresado en el paso 1. usando la función eval() vamos a almacenar el  resultado  
        resultado = eval(instrucción)    
  
        # 3. Mostraremos en pantalla el resultado obtenido en el paso 2.  
        print(resultado)  


El código de calculadora-2.py de esta disponible `aquí <https://github.com/lnds/programando.org/blob/master/curso-de-programacion-cap-9-funciones/calculadora-2.py>`_.

El siguiente es un pantallazo obtenido al ejecutar calculadora-2.py en mi equipo:

.. figure:: /_static/probando-calculadora-2.png
   :scale: 80 %
   :alt: probando calculadora 2
   :align: center

Bien, eso es todo por esta vez, vamos a los ejercicios, recuerda practicarlos.

Ejercicios
----------

        #. Escribe las funciones: kelcel, y celkel para convertir de grados Kelvin a Celsius.
	#. Modifica el programa calculadora-2.py para incorporar las funciones creadas en el primer ejercicio.
	#. Crea una función kelfahr() y fahrkel() a partir de las funciones previas e incorpórala a la calculadora.
	#. Crea una función ayuda que llame a la función help() e incorporala a la calculadora. La función ayuda debe comportarse igual que la función ``help()``
	#. Crea una función ``area_triangulo(base, altura)`` que calcule el area de un triángulo. Crea las funciones para calcular el área de un círculo, un rectángulo y otras figuras geométricas y agrégalas a la calculadora. Cada función debe tener su documentación

