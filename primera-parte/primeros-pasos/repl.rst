8. REPL
=======

Hasta ahora hemos usado IDLE, nuestro ambiente interactivo de python, pero no hemos escrito ningún programa, ahora vamos a partir escribiendo un programa bien poderoso: nuestro propio ambiente interactivo de python (una especia de clon de IDLE).

La función `eval()`
-------------------

Ya hemos estado usando algunas funciones en nuestros anteriores capítulos. Por ejemplo, `bool(x)`, `int(x)`, `float(x)`, `str(x)`, `type(x)`. Las funciones son un conjunto de instrucciones encapsuladas, piensen como pequeños programas que ejecutan alguna operación con los argumentos que reciben y retornan un resultado.

Más adelante vamos a escribir nuestras propias funciones y ahí aclararemos los detalles. Ahora veamos 2 funciones bien especiales, la primera se llama  `eval()`, veamos que hace en IDLE: ::

    >>> eval('2+2')  
    4  
    >>> eval('2*(4+2)')  
    12  
    >>> pi = 3.1415  
    >>> eval('2*pi')  
    6.28  
    >>> eval('2*"pi"')  
    'pipi'  
    >>> eval('2*"ja"')  
    jaja  


Lo que hace la función `eval()` es interpretar la expresión que recibe como argumento (un string) y retornar el resultado de convertir ese string a una expresión python.

El argumento de `eval()` debe ser un string, si la expresión puede ser evaluada entonces eval retorna el valor correspondiente (fijate que el valor puede ser un string, un int, o un float, o lo que resulte de la evaluación de la expresión recibida como argumento).

Por cierto, si la expresión no puede ser evaluada correctamente `eval()` genera un error: ::

    >>> eval('2*ja')  
    Traceback (most recent call last):  
      File "  
    <pyshell#24>", line 1, in <module>  
        eval('2*ja')  
      File "<string>", line 1, in <module>  
    NameError: name 'ja' is not defined  
    </module></string></module></pyshell#24>  

Arriba el error se produce porque no existe la variable ja (no confundir con el string “ja”).

La función `eval()` tiene una limitación, no puedes crear nuevas variables con esta función. ::

    >>> eval('e = 2.71828')  
    Traceback (most recent call last):  
      File "  
    <pyshell#27>", line 1, in <module>  
        eval('e = 2.17828')  
      File "<string>", line 1  
        e = 2.17828  
          ^  
    SyntaxError: invalid syntax  
    </string></module></pyshell#27>  


La razón de esto la explicaremos más adelante, hay otros tipo de expresiones que tampoco se pueden evaluar, pero funciona bastante bien para todo el tipo de expresiones que hemos usado hasta ahora, salvo las asignaciones (*).

Entrada y Salida
----------------

Bien, ahora ya tenemos a nuestra disposición una poderosa función que nos permiten interpretar las expresioens contenidas en un string (eval()).

Estamos en condiciones de diseñar nuestro “programa clon de IDLE”.: ::


	1. Necesitamos leer la instrucción que el usuario quiere ejecutar, y la guardaremos en un string
	2. Evaluaremos el string ingresado en el paso 1. usando la función eval() vamos a almacenar el resultado.
	3. Mostraremos en pantalla el resultado obtenido en el paso 2.
	4. Volveremos al paso 1. 

¿Como podemos implementar el paso 1 de nuestro programa?

Para eso tenemos la función `input()`. ::

    >>> instrucción = input()  
    2+2 <--- esto lo debes tipear tú  
    '2+2'  
    >>> instrucción  
    '2+2'  

La función input() se queda esperando a que ingreses un texto y presiones la tecla enter (intro).
Puedes usar un "prompt" junto con la función input: ::

    >>> instrucción = input('escribe tu expresión -->')  
    escribe tu expresión -->2*2  
    '2*2'  

El paso 2. de nuestro programa se ejecuta con la función `print()`. ::

    >>> instrucción = input()  
    2*pi <--- esto lo debes tipear tú  
    >>> print(instrucción)  
    2+pi  

Fíjense que print() elimina las comillas alrededor del texto: ::

    >>> print("Python viene de 'Monty Python Flying Circus' un programa de comedia inglés")  
    Python viene de 'Monty Python Flying' Circus un programa de comedia inglés  

Escribamos los 3 primeros pasos de nuestro programa pero en python: ::

    # 1. Necesitamos leer la <strong>instrucción</strong> que el usuario quiere ejecutar, y la guardaremos en un string  
    instrucción = input("-->")  
      
    # 2. Evaluaremos el string ingresado en el paso 1. usando la función eval() vamos a almacenar el  resultado  
    resultado = eval(instrucción)  
      
    # 3. Mostraremos en pantalla el resultado obtenido en el paso 2.  
    print(resultado)  


El símbolo # (numeral, o como le decimos en Chile 'gato') sirve para colocar un comentario que es ignorado por python.
Lo que hice fue escribir cada uno de los pasos de nuestro programa descrito antes y abajo su expresión en python.


Ingresar esto en IDLE directamente puede dar resultados confusos, así que vamos a abrir nuestro editor (notepad, notepad++, vi, Gedit, lo que quieras usar y vamos a escribirlo allí (* ver Nota 1)

.. figure:: /_static/clon-ide.py-image.png
   :scale: 50 %
   :alt: Nuestro primer programa en python cargado en Notepad++ 
   :align: center

   Nuestro primer programa en python cargado en Notepad++ (click para agrandar)


Este programa en particular lo grabaremos en un archivo que se llama clon-ide.py. Todos los archivos con programas python llevan la extensión .py por convención.

Hay varias formas de ejecutar este programa, si está bien instalado python en tu ambiente (en ubuntu o en windows) simplemente vas hasta la carpeta donde se encuentra tu programa y los ejecutas. En Windows basta con hacer doble click en el archivo. Este es el resultado que obtuve en mi PC:

.. figure:: /_static/pantalla-1-clon-idle.png
   :scale: 50 %
   :alt: Pantalla de ejecución clon idle
   :align: center

   Pantalla de ejecución clon idle (click para agrandar)

Fíjate que nuestro clon de IDLE usa el símbolo '-->' como prompt. Ahora vamos a probarlo, para eso escribiremos una expresión y luego presionaremos enter:

.. figure:: /_static/pantalla-2-clon-idle.png
   :scale: 50 %
   :alt: Ejecutando nuestro programa
   :align: center

   Ejecutando nuestro programa (click para agrandar)

El resultado puede ser frustrante, porque después de presionar ENTER la pantalla se cierra, y apenas alcanzamos a ver el resultado. Para remediar esto necesitamos completar el paso 4 de nuestro programa.

Loop
****


El paso 4 nos pide volver a ejecutar la secuencia 1, esto producirá un ciclo, es decir, llevará a repetir las instrucciones una y otra vez. Esto es lo que conocemos como un ciclo, bucle o loop.

En nuestro caso queremos ejecutar este ciclo para siempre (al menos hasta que alguien cierre la ventana donde se ejecuta). Estamos ante la presencia de lo que se conoce como un loop infinito. Es un tipo de construcción tan común que hay una manera estándar de escribirla en python: ::

	while True:  
	    instrucciones...

Fíjense que las instrucciones se escriben con una "sangría" de espacios en blanco, esto se conoce como `indentación <http://es.wikipedia.org/wiki/Indentaci%C3%B3n>`_ y es muy importante en python.

Veamos como queda nuestro programa ahora: ::

    while True: # loop infinito  
      
        # 1. Necesitamos leer la <strong>instrucción</strong> que el usuario quiere ejecutar, y la guardaremos en un string  
        instrucción = input("-->")  
      
        # 2. Evaluaremos el string ingresado en el paso 1. usando la función eval() vamos a almacenar el  resultado  
        resultado = eval(instrucción)  
      
        # 3. Mostraremos en pantalla el resultado obtenido en el paso 2.  
        print(resultado)  


Al ejecutar nuestro programa podemos interactuar con él y funciona bastante bien: 


.. figure:: /_static/clon-idle-en-ejecucion.png
   :scale: 50 %
   :alt: clon de idle en ejecución
   :align: center

   clon de idle en ejecución (click para agrandar)

REPL
----

Lo que hicimos en este post fue implementar lo que se conoce como REPL: `Read Eval Print Loop <http://en.wikipedia.org/wiki/Read-eval-print_loop>`_ (Ciclo Leer-Evaluar-Imprimir). Esta es una construcción muy poderosa, y útil, tanto que algunos proponen que la capacidad de implementar un REPL es una medida de la flexibilida y poder de un lenguaje de programación.

Bien, con esto terminamos nuestros primeros pasos exploratorios en python, vamos a partir de los próximos posts a empezar a programar realmente en python, han sido varios posts diarios, así que vamos a tener una pausa y volvemos, practiquen los ejercicios y experimenten con IDLE.


* Nota 1: los programas en python3 deben estar codificados en UTF-8, si usas Notepad++ anda a la opción del menú Formato y selecciona "Codificar en UTF-8".

Ejercicios
----------

#. Intenta escribir una declaración de variable al ejecutar el clon de IDLE. ¿Qué pasa? Investiga cuales son los límites de nuestro programa, que tipo de expresiones es incapaz de evaluar.

#. ¿Bajo qué condiciones falla este programa? ¿se te ocurre forma de corregirlo? (hint, ¿qué pasa si colocas un espacio en blanco al inicio de tu expresión?).

#. Modifica el programa para que el prompt (-->) sea algo más amistoso, como "ingresa tu expresión: " y antes del resultado ponga la frase "el resultado de tu expresión es: ".

#. Modifica el programa para que incorpore las variables "pre definidas" pi = 3.1415 y e = 2.71828 de modo que puedan ser usada en las expresiones. Es decir, después de esta modificación al ejecutar el programa se debe poder ejecutar la sesión interactiva que se muestra en este pantallazo:


.. figure:: /_static/clon-idle-modificado-en-ejecucion.png
   :align: center



