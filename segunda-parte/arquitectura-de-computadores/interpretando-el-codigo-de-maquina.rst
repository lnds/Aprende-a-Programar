19. Interpretando el código de máquina
======================================

En el capítulo anterior implementamos la función de carga `loader()`, la que nos permite leer un archivo con las instrucciones
del lenguaje assembler de nuestra máquina virtual y dejarlas en la memoria de nuestra cpu simulada.

Ahora corresponde ejecutar ese código.

La función del interprete
-------------------------

Un interprete es una función que toma las instrucciones en memoria y simula su ejecución, tal como lo haría una máquina real.
Por ejemplo, consideremos este fragmento de código assembler: ::

	 0. AR0
	 1. 5
	 2. AR1
	 3. 0
	 4. INCR1
	 5. RMUL
	 6. IMPR

Lo que hará el intérprete es lo siguiente: ::

	0. Cargar en una variable r0 el valor 5
	1. Cargar en una variable r1 el valor 0
	2. Incrementar el valor de la instruccion r1 en 1
	3. Multiplicar r0 por r1 y depositar el resultado en una variable acum
	4. Imprime el valor de la variable acum
	
Ese es el resultado final, pero la verdad es que nuestro intérprete va analizando una a una las instrucciones.

Por ejemplo, el fragmento de arriba es traducido a números en memoria, voy a escribir el código numérico y al lado, después del punto y coma, el código
assembler correspondiente, veamos: ::

	 16 ; AR0
	 5  ; 5
	 17 ; AR1
	 0  ; 0
	 22 ; INCR1
	 13 ; RMUL
	 6  ; IMPR

La parte de la interpretación de cada instrucción se podría implementar del siguiente modo: ::

	# supongamos que en la variable memoria tenemos las instrucciones cargas por loader
	# ademas ip es el instruction pointer que indica cual es la siguiente instrucción
	# a interpretar. Este fragmento de código interpreta las instrucciones 16 (AR0), 
	# 17 (AR1), 22 (INCR1), 13 (RMUL) y 6 (IMPR)
	
	if memoria[ip] == 16:
		ip = ip + 1
		r0 = memoria[ip]
		ip = ip + 1
	elif memoria[ip] == 17:
		ip = ip + 1
		r1 = memoria[ip]
		ip = ip + 1
	elif memoria[ip] = 22:
		r1 = r1 + 1
		ip = ip + 1
	elif memoria[ip] == 13:
		acum = r1 * r0
		ip = ip+1
	elif memoria[ip] == 6:
		print (acum)
		ip = ip + 1

Esto podría ser parte de una función que llamaremos `interpretar_instruccion()`, que sería una enorme serie de if parecidos
a lo de más arriba.

Pero hacer eso sería tedioso, y propenso a errores.

Para empezar, tendríamos que tener cuidado de no equivocarnos en los códigos de instrucciones, agregar un nuevo código significa
incorporar un if más, ¿qué pasa si decidimos reordenar nuestro juego de instrucciones, y en un momento la instruccion IMPR pasa a 
tener el código 8?.

Python tiene una manera más inteligente de hacer esto.

Funciones de orden superior
---------------------------

Hay una forma mejor aprovechando el hecho de que en Python las funciones son objetos, igual que los números, o los strings.
Así que nuestra función `interpretar_instruccion()` se podría escribir así: ::

	def interpretar_funciones():
		ip = funciones[memoria[ip]](memoria, ip)
		
¡QUÉ!

Lo que pasa es que hay cosas que nos les he contado.

Si recuerdan el capítulo anterior, teníamos un arreglo con los nemónicos de esta forma: ::

	nemonicos = ['ALTO','LIM','ACUM','MUL','RES','DIV','IMPR','LEER','ALM','REC','RR0','RR1','RSUM','RMUL','RRES','RDIV',
        'AR0','AR1','INC','DEC','INCR0','DECR0','INCR1','DECR1','SALTA','SSC','SSN','SSP','SRMA','SRME''SRIG']
		
y ¿que tal si tuvieramos una función por cada una de estas operaciones, las que dejamos en un arreglo de funciones? Del siguiente modo: ::

	funciones = [ALTO,LIM,ACUM,MUL,RES,DIV,IMPR,LEER,ALM,REC,RR0,RR1,RSUM,RMUL,RRES,RDIV,AR0,AR1,INC,DEC,INCR0,DECR0,INCR1,DECR1,SALTA,SSC,SSN,SSN,SRMA,SRME,SRIG]
	
entonces cada función se podría implementar por separado: ::

	def AR0(mem, ip):
		ip = ip + 1
		r0 = mem[ip]
		return ip + 1
	
	def AR1(mem, ip):
		ip = ip + 1
		r1 = mem[ip]
		return ip + 1
	
	def INCR1(mem, ip):
		r1 = r1 + 1 	
		return ip + 1

	def RMUL(mem, ip):
		acum = r0 * r1
		return ip + 1, acum, r0, r1
	
	
	def IMPR(mem, ip):
		print (acum)
		return ip + 1, acum, r0, r1


asi por ejemplo, si `memoria` e `ip` son mis variables que contienen los valores en memoria y el instruction pointer, respectivamente, y si el código
para el nemónico IMPR es el 6, entonces al hacer: ::

	funciones[6](memoria, ip)
	
es equivalente a a hacer: ::

	IMPR(memoria, ip)
	
porque el elemento 6 del arreglo `funciones` contiene a la función `IMPR()`.

La función CPU
--------------

Ahora estamos en condiciones de escribir nuestro simulador de CPU para la máquina virtual que definimos en el capítulo 17.

Siguiendo la idea planteada anteriormente, cada instrucción será implementada por una función. Cada función será de la forma: ::

	def INSTRUCCION(mem, ip, acum, r0, r1):
		...
		...
		return nuevo_ip, nuevo_acum, nuevo_r0, nuevo_r1

Es decir, una función que recibe la memoria, el instruction pointr, el registro acumulador, y los registros r0 y r1. Esta función 
debe retornar los nuevos valores que tendrán estos registros al salir.

El siguiente es parte del código de cpu.py, el programa que implementa nuestro simulador de CPU virtual: ::

	# arreglo de nemónicos	
	nemonicos = ['ALTO','LIM','ACUM','MUL','RES','DIV','IMPR','LEER','ALM','REC','RR0','RR1','RSUM','RMUL','RRES','RDIV',
        'AR0','AR1','INC','DEC','INCR0','DECR0','INCR1','DECR1','SALTA','SSC','SSN','SSP', 'SRMA','SRME''SRIG']
		

	# arreglo de funciones
	funciones = [ALTO,LIM,ACUM,MUL,RES,DIV,IMPR,LEER,ALM,REC,RR0,RR1,RSUM,RMUL,RRES,RDIV,AR0,AR1,INC,DEC,INCR0,DECR0,INCR1,DECR1,SALTA,SSC,SSN,SSN,SRMA,SRME,SRIG]


	TAM_MEMORIA = 1024 # tamaño en bytes de la memoria

	# loader, función de carga
	def loader(nombre_archivo):
		memoria = []
		archivo =open(nombre_archivo)
		lineas = archivo.readlines()
		for linea in lineas:
			codigo = linea.strip()
			if codigo in nemonicos:
				memoria.append(nemonicos.index(codigo))
			else:
				memoria.append(int(codigo))
		# la memoria tiene un tamaño de TAM_MEMORIA
		while len(memoria) < TAM_MEMORIA:
			memoria.append(0) # rellena con 0 la memoria
		return memoria

	# cpu es el simularor de cpu
	def cpu(archivo):
		memoria = loader(archivo)
		r0 = 0
		r1 = 0
		acum = 0
		ip = 0
		while ip >= 0:
			ip, acum, r0, r1 = funciones[memoria[ip]](memoria, ip, acum, r0, r1)
	
La función `ALTO` se encarga de retornar -1 (un valor imposible para IP), con esto obliga a cerrar el ciclo, las siguientes son las implementaciones
de las 30 instrucciones de nuestro lenguaje de máquina: ::

	def	ALTO(mem, ip, acum, r0, r1):
		return -1, acum, r0, r1
		
	def LIM(mem,ip, acum, r0, r1):
		acum = 0
		return ip + 1, acum, r0, r1
		
	def ACUM(mem, ip, acum, r0, r1):
		ip = ip + 1
		acum = acum + mem[ip]
		return ip + 1, acum, r0, r1
		
	def MUL(mem, ip, acum, r0, r1):
		ip = ip + 1
		acum = acum * mem[ip]
		return ip + 1, acum, r0, r1
		
	def RES(mem, ip, acum, r0, r1):
		ip = ip + 1
		acum = acum - mem[ip]
		return ip + 1, acum, r0, r1
		
	def DIV(mem, ip, acum, r0, r1):
		ip = ip + 1
		acum = acum / mem[ip]
		return ip + 1, acum, r0, r1
		
	def IMPR(mem, ip, acum, r0, r1):
		print (acum)
		return ip + 1, acum, r0, r1
		
	def LEER(mem, ip, acum, r0, r1):
		val = input()
		acum = val
		return ip + 1, acum, r0, r1
		
	def ALM(mem, ip, acum, r0, r1):
		ip = ip+1
		mem[mem[ip]] = acum
		return ip+1, acum, r0, r1
		
	def REC(mem, ip, acum, r0, r1):
		ip = ip+1
		acum = mem[mem[ip]] 
		return ip+1, acum, r0, r1
		
	def RR0(mem, ip, acum, r0, r1):
		ip = ip + 1
		r0 = mem[ip]
		return ip + 1, acum, r0, r1
		
	def RR1(mem, ip, acum, r0, r1):
		ip = ip + 1
		r1 = mem[ip]
		return ip + 1, acum, r0, r1

	def RSUM(mem, ip, acum, r0, r1):
		acum = r0 + r1
		return ip + 1, acum, r0, r1

	def RMUL(mem, ip, acum, r0, r1):
		acum = r0 * r1
		return ip + 1, acum, r0, r1
		
	def RRES(mem, ip, acum, r0, r1):
		acum = r0 - r1
		return ip + 1, acum, r0, r1
		
	def RDIV(mem, ip, acum, r0, r1):
		acum = r0 / r1
		return ip + 1, acum, r0, r1
		
	def AR0(mem, ip, acum, r0, r1):
		ip = ip + 1
		r0 = mem[ip]
		return ip + 1, acum, r0, r1
		
	def AR1(mem, ip, acum, r0, r1):
		ip = ip + 1
		r1 = mem[ip]
		return ip + 1, acum, r0, r1
		
	def INC(mem, ip, acum, r0, r1):
		acum = acum + 1
		return ip + 1, acum, r0, r1

	def DEC(mem, ip, acum, r0, r1):
		acum = acum - 1
		return ip + 1, acum, r0, r1
		
	def INCR0(mem, ip, acum, r0, r1):
		r0 = r0 + 1
		return ip + 1, acum, r0, r1
		
	def DECR0(mem, ip, acum, r0, r1):
		r0 = r0 - 1
		return ip + 1, acum, r0, r1
		
	def INCR1(mem, ip, acum, r0, r1):
		r1 = r1 + 1 	
		return ip + 1, acum, r0, r1
		
	def DECR1(mem, ip, acum, r0, r1):
		r1 = r1 - 1
		return ip + 1, acum, r0, r1
		
	def SALTA(mem, ip, acum, r0, r1):
		ip = ip + 1
		return mem[ip], acum, r0, r1
		
	def SSC(mem, ip, acum, r0, r1):
		ip = ip + 1
		if acum == 0:
			ip = mem[ip]
		else:
			ip = ip + 1
		return ip, acum, r0, r1
		
		
	def SSN(mem, ip, acum, r0, r1):
		ip = ip + 1
		if acum < 0:
			ip = mem[ip]
		else:
			ip = ip + 1
		return ip, acum, r0, r1

	def SSP(mem, ip, acum, r0, r1):
		ip = ip + 1
		if acum > 0:
			ip = mem[ip]
		else:
			ip = ip + 1
		return ip, acum, r0, r1

	def SRMA(mem, ip, acum, r0, r1):
		ip = ip + 1
		if r0 > r1:
			ip = mem[ip]
		else:
			ip = ip + 1
		return ip, acum, r0, r1

	def SRME(mem, ip, acum, r0, r1):
		ip = ip + 1
		if r0 < r1:
			ip = mem[ip]
		else:
			ip = ip + 1
		return ip, acum, r0, r1
		
	def SRIG(mem, ip, acum, r0, r1):
		ip = ip + 1
		if r0 == r1:
			ip = mem[ip]
		else:
			ip = ip + 1
		return ip, acum, r0, r1



En el `repositorio GitHub <https://github.com/lnds/programando.org>`_ 
de este curso encontrarás el código completo descrito en este capítulo, puedes  descargarlo desde 
`acá <https://github.com/lnds/programando.org/tree/master/curso-de-programacion-cap-19>`_.

Ejercicios
----------

	1. Fíjate que una función puede retornar más de un valor. La función swap(a,b) se define así: ::
		  def swap(a,b):
			  return b, a
	
	   explica para que serviría esta función.

	2. Explica como operan las siguientes dos funciones: ::

			def ALM(mem, ip, acum, r0, r1):
				ip = ip+1
				mem[mem[ip]] = acum
				return ip+1, acum, r0, r1
				
			def REC(mem, ip, acum, r0, r1):
				ip = ip+1
				acum = mem[mem[ip]] 
				return ip+1, acum, r0, r1

		¿Por qué crees que no retornamos mem?

	3. Prueba este programa con nuestro interprete y explica que sucede: ::
			INC
			INC
			ALM
			10
			LIM
			REC
			10
			IMPR
			ALTO
			
	4. Modifica el programa cpu.py de modo que imprima por pantalla el valor de la siguiente instrucción a interpretar y los valores
	de los distintos registros.
	
	5. Modifica el interprete para incorpora las instrucciones SR0, SR1 que saltan a la dirección indicada por el registro R0 y R1 respectivamente.