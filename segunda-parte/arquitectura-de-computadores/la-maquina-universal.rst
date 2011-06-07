16. La Máquina Universal
------------------------

En la primera parte de nuestro curso de programación aprendimos los elementos básicos para construir programas simples. 
Fuimos aprendiendo esto en la medida que ibamos construyendo un juego de naipes. Pero este juego tiene una interfaz de usuario 
bastante básica basada en texto. 

Aunque ustedes no lo crean un programa idéntico a este fue usado en un proyecto de juegos para telefonía móvil usando SMS. 
Del mismo modo se podría usar para jugar en twitter, las posibilidades están abiertas a vuestra imaginación como desarrolladores.

Sin embargo, creo que sería más interesante contar con una interfaz gráfica de usuario para nuestro juego, y después podemos 
extender nuestro juego para que sea jugado por muchas personas a través de la web. Así que la segunda parte de nuestro curso 
tiene por objetivo construir una versión gráfica del juego de BlackJack, para ser jugada en un computador personal con un sistema 
operativo moderno (como Ubuntu, Mac OSX, o Windows 7). En la tercera parte del curso llevaremos nuestro juego a la web.

Para poder lograr nuestro objetivo tenemos que aprender un poco más de cómo funcionan los computadores, y a esta exploración 
vamos a dedicar nuestras siguientes lecciones. Vamos a partir con un poco de historia, no se preocupen, no es aburrida, 
involucra algo de acción y espionaje, y drama humano.

La máquina universal
====================

.. figure:: /_static/Alan_Turing.jpg
   :scale: 30%
   :alt: Alan Turing
   :align: right
   
   Alan Turing, el padre de la computación
   
En 1931 un joven de 24 años, Alan Turing decidió reformular ciertos resultados de la lógica matemática expresando 
las formulaciones de teoremas en términos de algoritmos que podían ser interpretados por una máquina teórica.
Un algoritmo es ”un conjunto preescrito de instrucciones o reglas bien definidas, ordenadas y finitas que permite 
realizar una actividad mediante pasos sucesivos que no generen dudas a quien deba realizar dicha actividad.” O sea, un programa.

Lo que pretendía Turing era estudiar los límites de las máquinas que realizaban cálculos automáticos. 
Era un tiempo en que se estaban sentando las bases de cómo serían los computadores. 
Ya era posible contar con los elementos para construir estas máquinas y Turing quería ver cual era el poder de estas máquinas. 
Hasta que punto estas máquinas serían capaces de ayudarnos a resolver problemas complejos.
Turing describió una máquina teórica que manipula los símbolos escritos una larga cinta de acuerdo a una tabla de reglas. 
La máquina de Turing consta de un cabezal que puede leer y/o escribir en una cinta infinita de papel. 
La máquina puede realizar sólo las siguientes operaciones: avanzar el cabezal hacia la dercha, avanzar el cabezal hacia la izquierda, 
leer el contenido de una celda de la cinta, borrar el contenido de una celda y escribir en la cinta.

.. figure:: /_static/Maquina-de-Turing.png
   :scale: 60 %
   :alt: Maquina de Turing
   :align: center
   
   Representación artística de la Máquina de Turing
   
Con este dispositivo tan simple Turing  tuvo éxito en su empeño. No sólo sentó las bases teóricas para la construcción de estas máquinas, 
sino que estableció la formalización del concepto de algoritmo, lo que llevaría al desarrollo de los lenguajes de programación, 
descubrió la manera de determinar la complejidad de los problemas que pueden ser abordados por una máquina de este tipo, 
e incluso planteó un tipo de test para verificar operacionalmente una máquina es inteligente, el famoso `Test de Turing <http://es.wikipedia.org/wiki/Test_de_Turing>`_.

Es a partir de los trabajos de Turing que contamos con el concepto de máquina universal, capaz de resolver cualquier problema. 
Una máquina que es capaz de emular muchos de nuestros procesos mentales. 
Turing pensaba que era posible un día descubrir los algoritmos que gobiernan nuestra forma de ser y pensar, y que eso podría ser transferido a una máquina.
Polémico y todo, esta idea ha sido el motor de gran parte del desarrollo de la inteligencia artificial. 
Personalmente creo que Turing se equivocaba en esta idea, y probablemente, como `plantea Jaron Lanier <http://www.edge.org/3rd_culture/lanier/lanier_index.html>`_,  
los traumas y `problemas de la vida personal <http://www.lnds.net/blog/2011/03/galeano-sobre-alan-turing.html>`_ de Turing fueron los impulsores 
de esta obsesión del grán lógico inglés. Pero estamos divagando.

Lo importante es que entendamos que este concepto de **máquina universal** se concretó y hoy tenemos computadores en todas partes, 
en el refrigerador, en nuestros televisores, en el automóvil y nuestros teléfonos móviles. 
Todos tienen un computador, una máquina universal de Turing que gobierna sus acciones, que decide en forma algorítimica como reaccionar 
ante el nuevo estímulo que recogen desde el exterior.

Enigma y la guerra que lo cambió todo
=====================================

.. figure:: /_static/Enigma.jpg
   :scale: 50 %
   :alt: La máquina Enigma
   :align: right
   
   La máquina Enigma
   
Durante la segunda guerra mundial Turing se vió involucrado en un proyecto secreto de alto impacto, tan importante se considera este proyecto 
que se dice que gran parte del resultado de la guerra, y la  derrota final de los Nazis, se debe al trabajo de este selecto equipo de científicos. 

Durante ese tiempo Turing y el equipo de `Bletchey Park <http://www.bletchleypark.org.uk/>`_ trabajaron descifrando los mensajes secretos del ejército alemán. 

En esa época las fuerzas germánas contaban con  máquinas de encriptación muy poderosas, como `Enigma <http://en.wikipedia.org/wiki/Enigma_machine>`_ 
y la máquina `Lorenz <http://en.wikipedia.org/wiki/Lorenz_SZ_40/42>`_. La máquina Enigma era usada principalmente 
por la armada y los famosos submarinos u-boat alemanes. El grupo Hut 8 era el encargado de decodificar estos mensajes y a cargo de este 
estaba Alan Turing.

Con el fin de cumplir con su misión el equipo de Bletchey Park diseñó y construyó una serie de máquinas para ayudar en el trabajo de descifrado automático 
de los mensajes captados por los servicios de inteligencia.

Entre las máquinas construidas por los ingleses se encontraba el Colossus Mark 2, probablemente el primer 
computador digital semi programable.

.. figure:: /_static/Colossus.jpg
   :scale: 50 %
   :alt: Colossus Mark II
   :align: left
   
   Colossus Mark II

Mucho del trabajo de estas máquinas se mantuvo en secreto por años, y por esta razón fueron ignorados por mucho tiempo.

En esos tiempos los ingléses desarrollaron una serie de computadores, y el mismo Turing trabajó en el desarrollo de algunos de estos.

Todos los computadores de esa época eran programados mediante cableado, el concepto revolucionario vino desde el otro lado del atlántico 
y sentó las bases para la estructura de los modernos computadores.

Recordemos que simultáneamente al trabajo de los ingleses los norteamericanos estaban desarrollando el famoso proyecto Manhattan que llevaría a la creación 
de la primera bomba atómica.

En ese equipo de científicos se encontraban varias de las mentes más brillantes de la época y en particular dos nuevos e importantes personajes de 
nuestra historia, el físico y posterior premio Nobel Richard Feynmann, y el brillante matemático John Von Neumann.

La computadora humana de Feynmann
=================================

Richard Feynmann cuenta que necesitaban hacer complicados cálculos matemáticos y mientras no contaran 
con un computador decidieron hacerlo con ayuda de personal humano: ::

	“Desarrollamos el programa, pero no teníamos ninguna máquina para probarlo. De modo que lo que hicimos 
	fue llenar una habitación con chicas, cada una de ellas con una Marchant [una calculadora]. 
	Pero ella era el multiplicador, y ella era el sumador, y ésta elevaba al cubo; teníamos tarjetas, 
	tarjetas con índices y todo lo que ella hacía era elevar al cubo un número y pasárselo a la siguiente. 
	Ésta hacía de multiplicador, la siguiente hacía de sumador; recorríamos el ciclo, eliminábamos todos los errores. 
	Bien, así lo hicimos. Y resultó que podíamos hacerlo a gran velocidad. 
	Nunca antes se había hecho cálculo en serie; cualquiera que hubiera hecho cálculos antes 
	alguna vez había realizado todos los pasos por si mismo. 
	Pero Ford(*) tuvo una buena idea, la maldita cosa trabajaba mucho más rápidamente que de la otra forma, 
	y con este sistema llegamos a alcanzar una velocidad igual a la predicha para la máquina IBM: exactamente la misma.”
	
(*) Se refiere a Henry Ford y su idea del producción en serie.

.. figure:: /_static/JohnvonNeumann-LosAlamos.gif
   :scale: 50 %
   :alt: John Von Neumann
   :align: right
   
   John Von Neumann
   
Entre los hombres que estaban en Los Alamos en aquel tiempo se encontraba un brillante matemático de origen Húngaro: 
John von Neumann. Considerado un halcón, por sus visiones políticas y su involucramiento en el desarrollo de 
armas atómicas (como la bomba de hidrógeno), John von Neumman estableció la primera arquitectura efectiva 
para construir computadores que pudieran ser programados en forma efectiva, es decir, sin tanto cableado.

La principal idea que propuso Von Neumann fue que los datos y los programas fueran ambos almacenados en la memoria principal de la computadora.

La arquitectura de Von Neumann se decribe en el artículo `“The first draft report on the EDVAC” <http://qss.stanford.edu/~godfrey/vonNeumann/vnedvac.pdf>`_
y corresponde, esencialmente, a la arquitectura usada por la mayor parte de las computadoras que usamos en la actualidad:

.. figure:: /_static/Von_Neumann_architecture2.png
   :scale: 70 %
   :alt: la arquitectura de Von Neumann
   :align: center
   
   La arquitectura de Von Neumann
   
Von Neumann estableció que la memoria es una sola unidad que contiene el programa y los datos sobre los que actuará el computador. 
Existe un módulo que llamó la unidad de control (CU por control unit) que lee las instrucciones desde la memoria y las ejecuta una a una. 
Otra unidad llamada la unidad de lógica y aritmética (ALU por su sigla en inglés) se encarga de los cálculos. 
La ALU lee los datos de un cálculo y escribe los resultados en la memoria. 
Juntas la unidad de control (CU) y la unidad aritmético lógica (ALU) conforman la Unidad Central de Proceso (CPU). 
Para comunicarse con el exterior la CPU se enlaza a los dispositivos de entrada (INPUT), como los teclados, sensores, 
mouse, unidades  de disco, etc, y a los dispositivos de salida (OUTPUT) como las pantallas, impresoras, parlantes, etc. 

Más adelante vamos a aprender sobre este modelo en más detalle pues es esencial para lograr cumplir con los futuros proyectos de nuestro curso.

Los destinos diversos de dos hombres notables
=============================================

A pesar de que las contribuciones de Turing y Von Neumann fueron fundamentales para el desarrollo de las computadoras, 
no se puede imaginar dos tipos de personajes tan distintos.

Von Neumann desarrollo principalmente computadores para mejorar los cálculos necesarios para desarrollar la bomba atómica. 
Aunque hizo notables contribuciones en el ámbito de las matemáticas y la ciencia de la computación. 
Ayudó a desarrollar el método de Montecarlo y varias técnicas de simulación con números seudoaleatorios 
(el algoritmo de números aleatorios que usamos en nuestro juego viene de los trabajos de este matemático). 
Es probablemente el científico que más influyó en el establecimiento del concepto de destrucción mutua asegurada, 
que estableció el equilibrio en términos nucleares entre las super potencias durante el periodo de la guerra fría. 

El favorecía la idea de un ataque nuclear preventivo a la Unión Sovietica para evitar que esta potencia adquiriera 
la bomba atómica. Von Neumann murió de cancer. Sus biógrafos han escrito: *”cuando von Neumann se enteró de que estaba 
incurablemente enfermo, su lógica le forzaba a darse cuenta de que cesaría de existir, y por tanto que cesaría de tener 
pensamientos…Su amigo Edward Teller dijo, ‘Pienso que von Neumann sufrió más cuando su mente dejo de funcionar que lo 
que había nunca visto sufrir a ningún ser humano’. El sentido de la invulnerabilidad de von Neumann, o simplemente el 
deseo de vivir se enfrentaba con hechos inalterables. Pareció tener un gran miedo de morir hasta el final… 
Ningún logro y ninguna clase de influencia podían salvarle ahora, como había tenido siempre en el pasado. 
Johnny von Neumann, que supo como vivir tan plenamente, no supo como morir.”*

Alan Turing siguió investigando en diversos temas, en 1952 escribió un `programa de ajedrez <http://www.lnds.net/blog/2008/01/ajedrez.html>`_, 
pero era imposible correrlo en ningún computador de esa época, y el actuaba como CPU humana. 
Sus últimos años los dedicó a la biología matemática, tratando de entender por que se daban 
secuencias de números de fibonacci en las estructuras vegetales. Alan Turing era homosexual, 
una condición que era condenada en la Inglaterra de los 1950s. Durante el proceso en que se 
investigaba una denuncia que él mismo interpuso por robo, tuvo que confesar su homosexulidad 
y el acusador pasó a ser acusado de “indecencia grave y perversión sexual”. La opción era ir 
a prisión o someterse a un tratamiento hormonal, que incluía la inyección de estrógeno, lo 
que le provocó la aparición de pechos, impotencia y otras molestias. En 1954 muere por 
envenenamiento por cianuro al comer una manzana. El acto se considera oficialmente un 
suicidio, pero su madre insistió en que fue un accidente.

Los fundamentos
===============

Si recuerdan la idea del computador humanos de Feynmann, podrán ver que las tarjetas que pasaban las operadoras corresponden 
a la memoria, las chicas con sus calculadoras correspondían a la unidad lógico aritmética, y Feynman y sus colegas actuaban 
como unidad de control. No es necesario saber de micro chips, o relés, para entender como funcionan los computadores.

Esta breve disgresión histórica tiene por objetivo presentarles un modelo de computador básico. El modelo de Von Neumman y 
la máquina de Turing sirven para entender en forma conceptual cómo operan los computadores. Seguiremos explorando esto 
en los próximos capítulos.

Lecturas recomendadas
=====================

	* `The Annotated Turing: A Guided Tour Through Alan Turing’s Historic Paper on Computability and the Turing Machine <http://www.amazon.com/gp/product/0470229055/ref=as_li_tf_tl?ie=UTF8&tag=lanaturaledel-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0470229055>`_
	  por Charles Petzolds, para entender el artículo original de Alan Turing.
	
	* Una historia sobre la máquina Enigma se encuentra en este sitio: `Kriptópolis la máquina Enigma <http://www.kriptopolis.org/la-maquina-enigma>`_
	
	* Este `video <http://www.lnds.net/blog/2010/06/la-maquina-de-turing-explicada-por-el-mismo-turing.html>`_ es un fragmento de 
	  la película `Breaking The Code <http://www.imdb.com/title/tt0115749/>`_, donde Turing explica el concepto detrás de la máquina de Turing.
	
	* Una biografía de Von Neumman se encuentra en `este sitio <http://www.astroseti.org/articulo/4101/biografia-de-john-von-neumann>`_, 
	  de donde sacamos algunas citas.
	
	* “El Placer de Descubrir” por Richard Feynman, Editorial Crítica Barcelona, año 2000.
	
