12. Juegos de azar
==================

Seguimos explorando python con el fin de armar nuestro juego de blackjack. En la lección anterior generamos nuestros naipes. Ahora vamos a barajar nuestras cartas.

El acto de barajar consiste en mezclar las cartas de modo que cuando se repartan salgan en la forma más aleatoria (al azar) posible. Finalmente la idea de barajar es desordenar las cartas para repartirlas. Lo que vamos a construir al final de este capítulo es una función que nos permita obtener cartas al azar de una baraja.

Dados y números aleatorios
--------------------------

.. figure:: /_static/dados.jpg
   :scale: 80 %
   :alt: diversos tipos de dados
   :align: right

Si tenemos un dado normal, de 6 caras, podemos tirarlo y con esto obtener un valor entre 1 y 6. Hay dados con 4, 6, 8, 10, incluso de 20 caras, como los de la figura.

Si tuvieramos una baraja nueva, ordenada, una alternativa a revolverlas sería tener un dado de 52 caras, tirarlo y elegir la carta de acuerdo al número que salga. Por ejemplo, si sale el 11, entonces tomamos la carta número 11 y la retiramos del naipe.

Pero, ¿como obtenemos ese dado? Bueno existe una función que sirve para eso. Esta función no es una función de las predefinidas de python, en este caso se trata de una función que se encuentra dentro de un módulo.

Por ahora vamos a definir un módulo como un conjunto de funciones que se encuentran agrupadas por conveniencia. En este caso el módulo se llama random (una palabra en inglés que significa azar, aleatorio).

Para usar un módulo usamos la instrucción import. Exploremos random en IDLE: ::

	>>> import random  
	>>> dir(random)  
	['BPF', 'LOG4', 'NV_MAGICCONST', 'RECIP_BPF', 'Random', 'SG_MAGICCONST', 'SystemRandom', 'TWOPI', '_BuiltinMethodType', '_MethodType', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__name__', '__package__', '_acos', '_ceil', '_collections', '_cos', '_e', '_exp', '_inst', '_log', '_pi', '_random', '_sha512', '_sin', '_sqrt', '_test', '_test_generator', '_urandom', '_warn', 'betavariate', 'choice', 'division', 'expovariate', 'gammavariate', 'gauss', 'getrandbits', 'getstate', 'lognormvariate', 'normalvariate', 'paretovariate', 'randint', 'random', 'randrange', 'sample', 'seed', 'setstate', 'shuffle', 'triangular', 'uniform', 'vonmisesvariate', 'weibullvariate']  
	>>> help(random)  
	Help on module random:  
	  
	NAME  
	    random - Random variable generators.  
	  
	DESCRIPTION  
		integers  
		--------  
		       uniform within range  
	  
		sequences  
		---------  
		       pick random element  
		       pick random sample  
		       generate random permutation  
	  
	       ....  

El comando ``dir(random)`` nos entrega la lista de ‘atributos’ del módulo. Más adelante detallaremos que es esto, pero básicamente nos entrega una lista, entre otras cosas, de las funciones que están contenidas en el módulo. Por supuesto puedes escribir ``help(random)`` y obtener una explicación más detallada de las funciones que hay en random.

Fíjense que en la explicación que entrega ``help(random)`` tenemos que para las secuencias puede tomar un elemento aleatorio, o tomar una muestra aleatoria. Las funciones de random que hacen esto son ``choice()`` y ``sample()``.


Probemos esto en IDLE, primero debes cargar la función que definimos en la lección anterior. 

.. code-block:: python
   :linenos:
   
   >>> generar_baraja():  
           palos = ['C', 'D', 'T', 'P']    
	  
	   valores = ['A'] + [v for v in range(2,11)] + ['J', 'Q', 'K']    
	  
	   return [(valor, palo) for palo in palos for valor in valores]    
	  
   >>> baraja = generar_baraja()  
	  
   >>> import random  
   >>> random.choice(baraja)  
	(7, 'T')  
   >>> random.choice(baraja)  
	(6, 'C')  
   >>> random.sample(baraja, 2)  
	[(2, 'T'), (6,'D)]

Estas dos funciones son bastante útiles, salvo por una cosa, la baraja sigue quedando igual, cuando repartimos cartas vamos retirando las cartas de la baraja.

Para eliminar un elemento de una lista tenemos la función remove, este es un tipo de función especial, la llamamos método y se aplica directamente sobre el objeto que queremos operar, veamos como: 

.. code-block:: python
   :linenos:

   >>> carta = random.choice(baraja)  
   >>> carta  
	(3, 'P')  
   >>> baraja.remove(carta)  
   >>> len(baraja)  
	51  
   >>> baraja  
	[('A', 'C'), (2, 'C'), (3, 'C'), (4, 'C'), (5, 'C'), (6, 'C'), (7, 'C'),  
	(8, 'C'), (9, 'C'), (10, 'C'), ('J', 'C'), ('Q', 'C'), ('K', 'C'),  
	('A', 'D'), (2, 'D'), (3, 'D'), (4, 'D'), (5, 'D'), (6, 'D'), (7, 'D'),  
	(8, 'D'), (9, 'D'), (10, 'D'), ('J', 'D'), ('Q', 'D'), ('K', 'D'),  
	('A', 'T'), (2, 'T'), (3, 'T'), (4, 'T'), (5, 'T'), (6, 'T'), (7, 'T'),  
	(8, 'T'), (9, 'T'), (10, 'T'), ('J', 'T'), ('Q','T'), ('K', 'T'),  
	('A', 'P'), (2, 'P'), (4, 'P'), (5, 'P'), (6, 'P'), (7, 'P'),  
	(8, 'P'), (9, 'P'), (10, 'P'), ('J', 'P'), ('Q', 'P'), ('K', 'P')]  

En la linea 14 pueden apreciar que falta la dupla ``(3, ‘P’)`` y que el tamaño de la baraja se redujo en 1.

Generadores
***********

Bien, ahora tenemos los elementos para construir una función que nos entregue una baraja “desordenada”. Para esto vamos a usar una técnica llamada función generadora o simplemente generador.

Mira este código:

.. code-block:: python
   :linenos:

   import random  
  
   def baraja_mezclada():  
       baraja = generar_baraja() # definida en la lección anterior  
       while len(baraja) > 0:  
           carta = random.choice(baraja)  
           baraja.remove(carta)  
           yield carta 

Lo que hace esta definición es crear un **generador**. Un generador es un tipo especial de objeto que puede ser usado para generar secuencias de datos. Este generador primero llama a ``generar_baraja()`` para obtener una baraja ordenada. Luego empieza un loop, este loop ``while`` ya lo conocemos, pero en vez de colocar ``True``, este loop tiene una condición que hace que este loop no sea infinito, esta condición es que el tamaño de la baraja sea mayor que 0, es decir, mientras tengamos una carta en la baraja ejecutaremos la secuencia de instrucciones que siguen. 
En el cuerpo del loop (lineas 6 a 8)  lo primero que hacemos es obtener una carta al azar de la baraja, luego la removemos de la baraja.

La ultima instrucción es nueva, ``yield`` es similar a ``return``, pero lo que hace es retornar un valor, pero en cierta forma deja marcado el generador de modo que la próxima vez que sea invocado continua el ciclo.

Probemos nuestra función generadora: ::


	>>> cartas = baraja_mezclada()  
	>>> cartas  
            <generator object="" baraja_mezclada="" at="" 0x0000000002ee8120="">  
	>>> [carta for carta in cartas]  
	[(6, 'P'), (8, 'C'), (8, 'P'), (10, 'P'), ('J', 'P'), ('K', 'C'), (6, 'T'),  
	(7, 'P'), (4, 'T'), (3, 'P'), ('J', 'D'), (7, 'C'), (3, 'D'), ('Q', 'T'),  
	('Q', 'C'), (3, 'C'), ('A', 'P'), (2, 'T'), ('Q', 'P'), (6, 'D'), (8, 'T'),  
	(7, 'D'), ('Q', 'D'), ('A', 'C'), ('J', 'C'), (5, 'D'), ('K', 'T'), ('K', 'P'),  
	('A', 'D'), (5, 'P'), (2, 'P'), (2, 'D'), (9, 'P'), (8, 'D'), (2, 'C'),  
	(7, 'T'), (5, 'T'), ('K', 'D'), (4, 'C'), (9, 'T'), (5, 'C'), (3, 'T'),  
	(10, 'T'), ('A', 'T'), (10, 'C'), (9, 'C'), (4, 'D'), (6, 'C'), (9, 'D'),  
	(10, 'D'), ('J', 'T'), (4, 'P')]  
	>>> [carta for carta in cartas]  
	[]  
	>>> naipes = baraja_mezclada()  
	>>> [naipe for naipe in naipes][0:4]  
	[(10, 'D'), (10, 'P'), ('A', 'C'), (3, 'P')]  

Esto de los generadores puede resultar un tanto confuso, así que les sugiero ejecutar los ejercicios para comprender mejor mediante la experimentación.

Ejercicios
----------

	#. Escribe una función que simule el lanzamiento de 2 dados.
	#. Escribe un generador que genere una secuencia de numeros pares desde 2 a 100
	#. Escribe un generador que funcione igual que la funcion range()
	#. Escribe un generador pares(n) que genere los numeros pares hasta n inclusive
	#. El módulo random tienen una función shuffle, investiga que hace y úsala para reescribir la función baraja_mezclada()
	#. Escribe un generador para simular una serie de lanzamientos de un par de dados

