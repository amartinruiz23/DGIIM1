# TEMA 2. Introducción a los sistemas operativos

## Índice
- [1. Componentes de un Sistema Operativo (SO) multiprogramado](#1-componentes-de-un-sistema-operativo-multiprogramado)
	- [1.1 Sistemas multiprogramados y de tiempo compartido](#11-sistemas-multiprogramados-y-de-tiempo-compartido)
	- [1.2 Monoprograma o procesamiento en serie](#12-monoprograma-o-procesamiento-en-serie)
	- [1.3 Sistemas en lotes sencillos o Sistemas Batch](#13-sistemas-en-lotes-sencillos-o-sistemas-batch)
	- [1.4 Sistemas en lotes multiprogramados](#14-sistemas-en-lotes-multiprogramados)
	- [1.5 Sistemas de tiempo compartido](#15-sistemas-de-tiempo-compartido)
	- [1.6 Procesos](#16-procesos)
		- [1.6.1 Concepto de proceso](#161-concepto-de-proceso)
	- [1.7 Implementación de procesos típica](#17-implementación-de-procesos-típica)
	- [1.8 Bloque de control de un proceso (PCB, Process Control Block)](#18-bloque-de-control-de-un-proceso-pcb-process-control-block)
	- [1.9 Estados de los procesos](#19-estados-de-los-procesos)
		- [1.9.1 Modelo de proceso de dos estados](#191-modelo-de-proceso-de-dos-estados)
		- [1.9.2 Llamadas al sitema](#192-llamadas-al-sistema)
		- [1.9.3 Modelo de los cinco estados](#193-modelo-de-los-cinco-estados)

- [2. Descripción y control de procesos](#2-descripción-y-control-de-procesos)
	- [2.1 Descripción de procesos: PCB](#21-descripción-de-procesos-pcb)
	- [2.2 Control de procesos](#22-control-de-procesos)
		- [2.2.1 Modo de ejecución del procesador](#221-modo-de-ejecución-del-procesador)
		- [2.2.2 Operación de cambio de modo](#222-operación-de-cambio-de-modo)
		- [2.2.3 Pasos en la operación de cambio de ususario a kernel](#223-pasos-en-la-operación-de-cambio-de-usuario-a-kernel)
		- [2.2.4 Operación de cambio de contexto (cambio de proceso)](#224-operación-de-cambio-de-contexto-cambio-de-proceso)
		- [2.2.5 Pasos en una operación de cambio de contexto (Dispatcher)](#225-pasos-en-una-operación-de-cambio-de-contexto-dispatcher)

- [3. Hebras (hilos)](#3-hebras-(hilos))
	- [3.1 Concepto de Hebra (hilos)](#31-concepto-de-hebra-hilos)
	- [3.2 Modelo de cinco estados para hebras](#32-modelo-de-cinco-estados-para-hebras)
	- [3.3 Ventajas de las hebras](#33-ventajas-de-las-hebras)

- [4. Gestión básica de memoria](#4-gestión-básica-de-memoria)
	- [4.1 Carga absoluta y reubicación](#41-carga-absoluta-y-reubicación)
	- [4.2 Reubicación estática](#42-reubicación-estática)
	- [4.3 Reubicación dinámica](#43-reubicación-dinámica)
	- [4.4 Espacios para las direcciones de memoria](#44-espacios-para-las-direcciones-de-memoria)
	- [4.5 Problema de la fragmentación de memoria](#45-problema-de-la-fragmentación-de-memoria)
	- [4.6 Solución a la fragmentación de memoria](#46-solución-a-la-fragmentación-de-memoria)
		- [4.6.1 Paginación](#461-paginación)
		- [4.6.2 Segmentación](#462-segmentación)

- [5. Compiladores](#5-compiladores)
	- [5.1 Resumen](#51-resumen)

## 1. COMPONENTES DE UN SISTEMA OPERATIVO MULTIPROGRAMADO

### 1.1 Sistemas multiprogramados y de tiempo compartido
Como el mejor sitio por donde empezar es el principio, comencemos con una breve evolución de las computadoras, hasta un sistema multiprogramado:

1. **Raimundo Lulio** en el siglo XII escribió *Ars Magna*, en el que se dedicó a diseñar y
construir una máquina lógica de naturaleza mecánica, donde las teorías, los sujetos y los predicados
teológicos estaban organizados en figuras geométricas de las consideradas "perfectas".

2. **Leibnitz**, en 1650 construye la primera máquina que multiplica, cuando descubre *Ars magna*
empieza a trabajar en la primera de algoritmo.

3. **Babbage** a principio del siglo XIX construye la primera máquina que procesa información.

4. A mediados del mismo siglo las matemáticas se empiezan a formalizar y estructurarse,
considerándose un fin por sí mismas, surgiendo los axiomas de Peano, lógica... Todo gracias a
personas y asociaciones como: **David Hilbert** y en 1950 **Burbaki**. Gracias a este movimiento,
**Turing** crea las "máquinas de Turing" y posteriormente "la máquina universal de Turing" que
podría considerarse uno de los precursores del ordenador.

5. A este ritmo los ordenadores iban surgiendo de manera natural. **A. Church** saca la máquina de cálculo **Post** y comienzan a aparecer los nuevos paradigmas: operacionales, funcionales y lógicos.

6. Surge el primer ordenador, **Colosus** para generar tablas de tiro, más tarde los ingleses lo utilizaron para manejar la información de los radares, aunque no se sabe si el primero fue alemán por los archivos encontrados tras su muerte a **Kamrao Zure** ingeniero para el ejército alemán durante la primera guerra mundial.

Aquí se acaba la historia con personajes y comienza la evolución de la arquitectura de los
computadores:

### 1.2 Monoprograma o procesamiento en serie

La más arcaica, requiere de mucho tiempo, el programador tenía interacción directa con el hardware, (no existía el Sistema Operativo) si había un error el programa se detenía.

Estas máquinas eran utilizadas desde una consola que contenía luces, interruptores, algún dispositivo de entrada y una impresora. Los programas en código de máquina se cargaban a través del dispositivo de entrada. Si un error provocaba la parada del programa, las luces indicaban la condición de error. El programador podía entonces examinar los registros del procesador y la memoria principal para determinar la causa de error. Si el programa terminaba de forma normal, la salida aparecía  en la impresora.

Problemas principales de estos sistemas:
- **Panificación** Las instalaciones contaban con plantillas impresas de reserva de tiempo, tiempo limitado (múltiplos de media hora). Por lo que se malgastaba el tiempo de procesamiento del computador.
- **Tiempo de configuración** Un trabajo (único programa) implicaba:
  1. Carga en memoria compilador y lenguaje de alto nivel (programa en código fuente).
  2. Carga y enlace del programa objeto y funciones comunes.
Estos pasos suponían montar y desmontar cintas o configurar tarjetas. Si ocurría un error, el usuario tenía que volver al comienzo de la secuencia de configuración. Lo que significa un tiempo elevado de configuración del programa que se va a ejecutar.

Se han desarrollado varias herramientas de software de sistemas con el fin de realizar el procesamiento serie más eficiente: bibliotecas de funciones comunes, enlazadores, cargadores, depuradores, rutinas de gestión de E/S disponibles como software común para todos los usuarios…

### 1.3 Sistemas en lotes sencillos o Sistemas Batch
El primer sistema operativo en lotes (y también el primer sistema operativo de cualquier tipo) surge en deseo de maximizar la utilización de las máquinas.
La idea central se basaba en una pieza de software denominada **monitor**: el usuario no tiene que acceder directamente a la máquina, sino que introduce el trabajo por medio de una tarjeta o cinta al operador del computador, que crea un sistema de lotes con los trabajos enviados y los coloca en el dispositivo de entrada para que los utilice el monitor. Cuando un programa finaliza su procesamniento devuelve el control al monitor, que comenzará la carga del siguiente programa.

Análisis de este esquema desde distintos puntos de vista:
- **Punto de vista del monitor**: controla la secuencia de eventos desde la memoria principal, siempre disponible para su ejecución. Esta porción del monitor es denominado **monitor residente**. El resto del monitor está formado por conjunto de utilidades y funciones comunes que se encargan como subrutinas al comienzo del programa del usuario.
  El monitor lee de uno en uno los trabajos desde el dispositivo de entrada (lector de tarjetas o dispositivo de cinta magnética), coloca el trabajo en el área de programa de usuario, y se le pasa el control, que cuando ha terminado le devuelve el control al monitor, que lee el siguiente trabajo. Los resultados de cada trabajo se envían a un dispositivo de salida (impresora) para entregárselo al usuario.
<img src="media/tema2/monitor_residente.png" width="250" height="300">

- **Punto de vista del procesador**: el procesador ejecuta instrucciones de la zona de memoria principal que contiene el monitor. Por lo que se lee el siguiente trabajo y se almacena en otra zona de memoria principal. El procesador encontrará una instrucción de salto en el monitor que le indica al procesador que continúe la ejecución al inicio del programa de usuario. El procesador entonces ejecutará las instrucciones del programa usuario hasta que encuentre una condición de finalización o de error. Cualquiera de estas condiciones hace que el procesador ejecute la siguiente instrucción del programa monitor. Por tanto, la frase “se pasa el control al trabajo” significa que el procesador leerá y ejecutará instrucciones del programa de usuario, y la frase “se devuelve el control al monitor” indica que el procesador leerá y ejecutará instrucciones del programa monitor.
Cuando el "control" lo tiene el monitor, ejecutará sus instrucciones y cuando no las del programa. El papel del monitor es de planificación, incluyendo intruccines en algún lenguaje primitivo de **lenguaje de control de trabajos** (JCL)

En resumen: El monitor o sistema operativo en lotes es un programa, que tiene en base, la habilidad del procesador para cargar instrucciones de memoria principal y tomar y abandonar el control.

Necesita también un hardware con: protección de memoria, temporizador de trabajos, instrucciones privilegiadas que solo el monitor puede realizar e interrucciones.
La protección de memoria y los privilegios dan lugar a los modos ususario y núcleo.
 El problema de la programación en lotes  era el tiempo que empleaba el ordenador en los periféricos.

### 1.4 Sistemas en lotes multiprogramados
En los trabajos automáticos de un sistema operativo en lotes simples el procesador se encuentra frecuentemente parado ya que los dispositivos de entrada y salida son mucho más lentos que este, así es como surge la **multiprogramación** o **multitarea**, se expande la memoria para que pueda albergar al sistema operativo (monitor residente) y más programas habiendo multiplexación entre ellos.
Al haber varios programas a la vez podría haber un solapamiento del trabajo, para evitar esto, surgen las **interrupcciones** de la mano de un avance de sofware y hardware, en el cual varios programas se desarrollan a la vez en sitios diferentes,  esto se conoce como **S.pool**: cualquier trabajo puede suspender su actividad por la ocurrecia de un evento definido, como la finalización de una operación E/S. El procesador guardaría alguna forma de contexto (contador de programa u otros registros) y saltaría a una rutina de tratamiento de interrupciones: determinaría tipo interrución, la procesaría y continuaría con el proceso interrumpido. Por ejemplo si varios porgramas requieren de una impresora, el programa que se está ejecutando escribe en un fichero lo que quiere imprimir y después lo vuelca a esta una vez que ha terminado de utilizar la impresora el programa anterior.

### 1.5 Sistemas de tiempo compartido  
Teniendo en cuenta que los lotes son cerrados surgen las **colas**, sistemas de lotes abiertos, donde el SO controla los programas que esperan y los que se ejecutan, y cuándo termina estos dan pasos a los siguiente en orden de prioridad. Por tanto, si un programa no utilizaba periféricos u otros recursos se podía quedar eternamente allí, o si era necesaria la interacción de varios usuarios directamente con la computadora, con esto surge la técnica  **del tiempo compartido**, los programas tienen un tiempo limitado en la CPU.  Estos intervalos de tiempo, también son conocidos como **cuantos de computación**.
Uno de los primeros sistemas operativos de tiempo compartido desarrollados fue el sistema CTSS (*Compatible Time-Sharing System*) desarrollado en el MIT por un grupo conocido como proyecto MAC y desarrollado para IBM.

 .| Multiprogramación en lotes           | Tiempo compartido
  ---		       | --- 		      		      | ---
 **Objetivo principal**    | Maximizar el tiempo del procesador   | Minimizar el tiempo de respuesta
 **Fuente de directivas<br>del sistema operativo** | Mandatos del lenguaje de control<br> de trabajos proporcionadas por el trabajp | Mandatos introducidos al terminal.

5. **Multiusuarios** misma idea anterior pero con usuarios, vg: servidores.

6. **Multiprocesadores** más de varias CPU en un mismo ordenador, pueden trabajar en distintas tareas o en **paralelo**, el mismo programa se divide en varios procesadores que trabajan simultáneamente.

7. Finalmente distintos ordenadores, con distintos sistemas operativos que trabajan simultáneamente, todos coordinados por un **macro sistema operativo**.


### Algunas preguntas
> !!! FALTAN POR COMPLETAR, LAS DEJO PARA QUE ALGUIEN LAS RELLENE

- La multiprogramación no tiene por qué ser de tiempo compartido. Pero para que sea posible el tiempo compartido es necesario un S.O. multiprogramado.
- Un S.O. multiprogramado es un S.O. de tiempo compartido? ¿y al contrario?  
- ¿Un S.O. de tiempo compartido tiene que ser multiusuario? ¿y monousuario?  
- ¿Un S.O. monoprocesador tiene que ser monousuario? ¿y multiusuario?  
- ¿Un S.O. multiprocesador tiene que ser monousuario? ¿y multiusuario?  


### 1.6 Procesos
#### 1.6.1 Concepto de proceso

Se han dado distintas definiciones de proceso, algunas: 
- Un programa en ejecución.
- Una instancia de un programa ejecutándose en un ordenador.
- La entidad que se puede asignar o ejecutar en un procesador.
- Una unidad de actividad caracterizada por un solo flujo de ejecución, un estado actual y un conjunto de recursos del sistema asociados.

El diseño del sofware de la multiprogramación era sumamente complejo, los programadores acudían a métodos *ad hoc* para  cooperación y coordinación de trabajos que generaba errores de : sincronización, violación de la exclusión mutua, operación no determinista de un programa, interbloqueos.

Para solucionar estos problemas se necesita una forma sistemática de monitorizar y controla la ejecucion de varios programas en el procesador y aquí es donde entra el concepto de proceso, conformado por:
- Un programa ejecutable
- Los datos asociados que necesita un programa.
- El contexto de ejecución de un programa o estado del proceso, que es el conjunto de datos internos separada del proceso por el cual el sistema operativo es capaz de supervisar y controlar el proceso y el procesador para ejecutarlo. Ejemplos: contador de programa, registro de datos, prioridad, estado...
<img src="media/tema2/proceso_tipico.jpg" width="300" height="350">

En la imagen, se muestra la manera de gestinar dos procesos, los contenidos de los registros de un programa que fue interrumpido fueron guardados en el contexto de ejecución del programa. Por esta razón un proceso puede verse como una estructura de datos, donde su **estado** se contiene en el contexto permitiendo así la cooperación  y la coordinación entre procesos.

> Notas de clase: 
>Cuando hay que leer de disco el sistema usuario no lee, los lenguajes dan sentencias, cuando se traducen son órdenes de llamadas de SO. El SO incorpora funciones propias donde corresponde al programa.
>Lo mismo con lenguajes fuertemente tipado, como hay cosas que el compilador no puede resolver en tiempo de compilación por falta de información, el compilador añade instrucciones al texto (*paquete de soporte a la ejecución*), para  poder ejecutarlo.  Así, se puede denominar *proceso* al programa original ejecutado, es decir quitando la lógica añadida por el SO.
>Ejemplo:
>Cuando, con el navegador abierto, se abre otra ventana del navegador,para cada ventanita hay una **instancia** con la sesión y la historia que guarda el navegador. Es decir, se tiene el mismo programa pero con varias instancias, es decir con distintos procesos. Podemos decir que un proceso o instancia es una ejecución particular del programa.

### 1.7 Implementación de procesos típica
Forma en la cual los procesos pueden gestionarse:
Dos procesos, A y B, se encuentran en una porción de memoria principal. Es decir, se ha asignado un bloque de memoria a cada proceso, que contiene el programa, datos e información de contexto. Se incluye a cada proceso en una lista de procesos que construye y mantien el SO. La lista de procesos contiene una entrada por cada proceso, e incluye un puntero a la ubicación del bloque de memoria que contiene el proceso. La entrada podría también incluir parte o todo el contexto de ejecución del proceso. El resto del contexto de ejecución es almacenado en otro lugar, tal vez junto al propio proceso o frecuentemente en una región de memoria separada. El registro índice del proceso contiene el índice del proceso que le procesador está actualmente controlando en la lista de procesos. El contador de programa apunta a la siguiente instrucción del proceso que se va a ejecutar. Los registros base y límite definen la región de memoria y el registro límite le tamaño de la región (en bytes o palabras). El contador de programa y todas las referencias de datos se interpretan de forma relativa al registro base y no deben exceder el valor almacenado en el registro límite. Esto previene la interferencia entre los procesos.
En la imagen anterior (Figura 2.8), el registro índice del proceso indica que el proceso B está ejecutando. El proceso A estaba ejecutando previamente, pero fue interrumpido temporalmente. Los contenidos de todos los registros en el momento de la interrupción de A fueron guardados en su contexto de ejecución. Posteriormente, el SO puede cambiar el proceso en ejecución y continuar la ejecución del contexto de A. Cuando se carga el contador de programa con un valor que apunta al área de programa de A, el proceso A continuará la ejecución automáticamente.

- Busca proceso en lista, le da la dirección recuper información con la que  carga la información,
- traza es lo que se pasa, en la CPU

>>Paula: que es esooo de arriba¿?¿???!?¿?!
>> Blanca: esooo es un apunte que tomé en clase y por ahora no sé bien donde meterlo

### 1.8 Bloque de control de un proceso (PCB, Process Control Block)
La memoria estaría llena de procesos o instancias. Así, el SO es el encargado de administrarlos de la forma correcta, para que todos sean ejecutados por el procesador de forma secuencial. Además, el SO tiene la capacidad de poder **bloquear un proceso**. Para que después pueda ser retomado como si nada, se  necesita información sobre cada proceso, lo que se conoce como **bloque de control de un programa* (BCP), consta de:

Elemento del bloque de control 	     | Descripción
--- 	     	       		     | ---
 **Identificador de proceso** <br> (PID *Process IDentificator*)|  Identificador único que se le asocia a un proceso.
 **Estado**      	 	     | En qué situación se encuentra el proceso en cada momento según el modelo de los cinco estados: preparado, bloqueado, preparado...
  **Prioridad**  	  	     | Nivel de prioridad relativo al resto de procesos, el SO, cuenta con algoritmos para modificarla 
  **Contador de programa** 	     | Dirección de la siguiente instrucción del programa  que se va a ejecutar.
  **Punteros a memoria**	     | Direcciones entre las que está un programa, dirección base y sus datos.
  **Datos de contexto** 	     | Datos del registro del procesador: registros que modifica, uso de  recursos, contador de programa, registros procesador...
  **Información del estado de E/S**  | Incluyes las peticiones pendientes de E/S, los dispositivos asignados a dichos procesos de E/S, lista de fichero en uso...
  **Información de auditoría** 	     | Inluye la cantidad de tiempo de de procesador y de reloj utilizados, limites de tiempo, registros contables...

La información de la lista anterior se almacena en una esctructura de datos (PCB), que el SO crea y gestiona. El PCB contiene suficiente información de forma que es posible interrumpir el proceso cuando está corriendo y restaurar su estado de ejecución. Cuando un proceso se interrumpe, los valores de datos de contexto, se guardan en los campos correspondientes, y el estado de proceso cambia, así el SO queda libre para poner otro proceso en estado de ejecución.
Por lo que un proceso está compuesto del código de programa, los datos asociados y del BCP.

### 1.9 Estados de los procesos
Se puede caracterizar el comportamiento de un determinado proceso, listando la secuencia de instrucciones que se ejecutan para dicho proceso (traza del proceso).
La figura 3.2 muestra el despliegue en memoria de tres procesos que no usan memoria virtual, por lo que están representador por programas que residen en memoria principal. Además, existe un pequeño programa activador (dispatcher) que intercambia el procesador de un proceso a otro.
La figura 3.3 muestra las trazas de cada uno de los procesos en los primeros instantes de ejecución. Se muestran las 12 primeras instrucciones ejecutadas por los procesos A y C. El proceso B ejecuta 4 instrucciones y se asume que la cuarta instrucción invoca una operación de E/S, a la cual el proceso debe esperar.
	Desde el punto de vista del procesador se entremezclan las trazas de ejecución de los procesos y las trazas del código del SO. Ejemplo de traza de ejecución:

<img src="media/tema2/estado_proceso.jpg" width="300" height="350">

#### 1.9.1 Modelo de proceso de dos estados
La responsabilidad principal del sistema operativo es controlar la ejecución de los procesos; esto incluye determinar el patrón de entrelazado para la ejecución y asignar recursos a los procesos. El primer paso en el diseño de un sistema operativo para el control de procesos es describir el comportamiento que se desea que tengan los procesos.
Se puede construir el modelo más simple posible observando que, en un instante  dado, un proceso está siendo ejecutado por el procesador o no. En este modelo, un proceso puede estar en dos estados: ejecutando ó no ejecutando. Cuando el SO crea un nuevo proceso, crea el BCP para el nuevo proceso e inserta dicho proceso en el sistema de estado no ejecutando. El proceso existe, es conocido por el SO, y está esperando su oportunidad y ejecutar. De cuando en cuando, el proceso actualmente en ejecución se interrumpirá y una parte del SO, el activador, seleccionará otro proceso.
Debe haber información correspondiente a cada proceso, incluyendo el estado actual y su localización en memoria: BCP. Los procesos que no están ejecutando deben estar en una especie de cola, esperando su turno para la ejecución. Existe una sola cola cuyas entradas son punteros al BCP de un proceso en particular. Alternativamente, la cola debe consistir en una lista enlazada de bloques de datos, en la cual cada bloque que representa un proceso. Si el proceso ha finalizado o ha sido abortado, se descarta (sale del sistema). En cualquier caso, el activador selecciona un proceso de la cola para ejecutar.

#### 1.9.2 Llamadas al sistema
>> J. Carretero, F. García, P. de Miguel, F. Pérez, Sistemas Operativos (2a Edición), McGraw-Hill,
2007i  páginas: 114-115

Por lo general, un sistema operativo está en un estado consistente y el código del servicio puede hacer uso de la funcionalidad general de un SO. Suele existir una única solicitud de interrucción de servicio, por lo que los servicioes empiezan ejecutando el mismo código.
El servicio puede requerir una espera (que bloquerá al proceso) como leer un disco o no, como cerrar un proceso.:
##### Cuando un servicio no requiere de espera:
- La intrucción **TRAP** genera la interrupción de petición de servicio.
- El procesador acepta la interrupción, por lo que el proceso pasa de mis usuario a modo usuario a modo privilegiado.
- A través de la tabla de interrupciones se ejecuta la rutina genérica que salva los registros visibles en la pila de sistema del proceso interrumpido. Seguidamente utiliza el identificador del servicio (almacenado en un registro) para entrar en la tabla de servicios y determina el punto de acceso del servicio solicitante.
- Llama al servicio y ejecuta el correspondiente código.
- Se retorna la rutina genérica que restituye los registros y en RETI, con lo que se devuelve la siguiente intrucción al TRAP.

Durante la ejecución de un servicio, pudo llegar una interrupción que pondría a ejecutar otro proceso.
<img src="media/tema2/ejecucion_servicio_sin_espera.jpeg" width="800" height="250">

#### Servivio que contiene espera
El tratamiento se divide en dos fases, una que inicial el servicio y otra que lo termina:
- La primera fase inicia el servicio (por ejemplo, lanza la oreden de lectura de un disco), ejecuta el planificador, el proceso queda bloqueado, y se pone en ejecución el proceso seleccionado, por lo que se produce un cambio de contexto.
- Más adelante un evento indica el fin de la espera (ejemplo: un disco completa una lectura y genera una interrupción), esta interrupción ejecutará el contexto de otro proceso y podrá tener una parte aplazada.
- Si la operación se completó con éxito el proceso pasa de bloqueado a listo.
- Cuando el planificador seleccione otra vez este proceso, seguirá la ejecución completando la segunda fase del servicio, (ejemplo: copiando buffer de la información leída en el disco).
- Finalmente se genera el argumento de retorno del servicio y se restituyen los registros visibles, y se retorna al proceso que sigue su ejecución en modo usuario.
<img src="media/tema2/ejecucion_servicio_con_espera.jpeg" width="800" height="250"> 
  

#### 1.9.3 Modelo de los cinco estados
>> stalling pag 114-120

Trata de representar las actividades que le SO lleva a cabo sobre los procesos:
- **Creación de un proceso:** cuando se va a añadir un nuevo proceso a aquellos que se están gestionando en un determinado momento, el SO construye las estructuras de datos que se usan para manejar el proceso y reserva el espacio de direcciones en memoria principal para el proceso.
	En un entorno por lotes, un proceso se crea como respuesta a una solicitud de trabajo. En un entorno interactivo, un proceso se crea cuando un nuevo usuario entra en el sistema. En ambos casos el SO es responsable de la creación de nuevos procesos.
	Razones para la creacion de un proceso:
	- **Nuevo proceso de lotes**: el SO dispone de un flujo de control de lotes de trabajos. Cuando el SO está listo para procesar un nuevo trabajo, leerá la siguiente secuencia de mandatos de control de trabajos.
	- **Sesión interactiva**: un usuario desde un terminal entra en el sistema.
	- **Creado por el sistema operativo para proporcionar un servicio**: el SO puede crear un proceso para realizar una función en representación de un programa de usuario, sin que el usuario tenga que esperar.
	- **Creado por un proceso existente**: por motivos de modularidad o para explotar el paralelismo, un programa de usuario puede ordenar la creación de un número de procesos.

	Cuando un SO crea un proceso a petición explícita de otro proceso, dicha acción se denomina **creación del proceso**.
	Cuando un proceso lanza otro, al primero se le denomina **proceso padre**, y al proceso creado se le denomina **proceso hijo**.

- **Terminación de procesos:** todo sistema debe proporcionar los mecanismos mediante los cuales un proceso indica su finalización, o que ha completado su tarea.
	Un trabajo por lotes debe incluir una instrucción HALT o una llamada a un servicio de SO específica para su terminación. Para una aplicación interactiva, las acciones del usuario indicarán cuándo el proceso ha terminado. Todas estas acciones tienen como resultado final la solicitud de un servicio al SO para terminar con el proceso solicitante.
	Adicionalmente, un número de error o una condición de fallo puede llevar a la finalización de un proceso.
	Razones para la terminación de un proceso:
	- **Finalización normal**
	- **Límite de tiempo excedido**
	- **Memoria no disponible**
	- **Violaciones de frontera**
	- **Error de protección**
	- **Error aritmético**
	- **Fallo de E/S**
	- **Instrucción no válida**

Por lo que para ello hace uso de cinco estados:
- **Ejecutando**: el proceso está actualmente en ejecución. Asumimos que el computador tiene un único procesador, de forma que solo un proceso puede estar en este estado en un instante determinado.
- **Listo o preparado**: un proceso que se prepara para ejecutar cuando tenga la oportunidad.
- **Bloqueado**: un proceso que no puede ejecutar hasta que se cumpla un evento determinado o se complete una operación E/S.
- **Nuevo**: un proceso que se acaba de crear y que aún no ha sido admitido en el grupo de procesos ejecutables por el SO. Se trata de un nuevo proceso que no ha sido cargado en memoria principal, aunque su BCP si ha sido creado.
- **Saliente**: un proceso que ha sido liberado del grupo de procesos ejecutables por el SO, debido a que ha sido detenido o que ha sido abortado por alguna razón. Si el programa termina de ejecutarse, el SO actualiza la lista de procesos y libera esa zona de memoria, eso se convierte en basura.

<img src="media/tema2/modelos_cinco_estados.png" width="350" height="350"> 

Cuando se carga un programa nuevo:
 - Instrucciones.
 - Datos: variables sin asignar un valor, estas tienen asignado un valor, basura, el que está en memoria de otro programa. Hay compiladores que te permiten ver en la parte derecha, y puede saber que no le has asignado ningún valor, cuando la vas a utilizar te avisan (otros no te dan ningún error ni en compilación ni en ejecución). Lo que sí se recomienta es trastear con el compilador. Hay compiladores que en el for la i la ponen, otros no la hacen, calculan el número de vueltas que hace el bucle. Otros, que si haces referencia dentro del buche a la i asocia sí lo tienen en cuennta, y si no, no. Te implementa la veces que se repite, esta variable se conoce como void variable **variable vacía** .


#### 1.9.3.1 Transiciones entre estados
- **Nuevo -> Preparado**: el PCB está creado y el programa está disponible en memoria.
- **Ejecutándose -> Finalizado**: el proceso finaliza normalmente o es abortado por el SO a causa de un error no recuperable.
- **Preparado -> Ejecutándose**: el SO (planificador CPU) selecciona un proceso para que se ejecute en el procesador.
- **Ejecutándose -> Bloqueado**: el proceso solicita algo al SO por lo que debe esperar.
- **Ejecutándose -> Preparado**: un proceso ha alcanzado el máximo tiempo de ejecución ininterrumpida.
- **Bloqueado -> Preparado**: se produce el evento por el cual el SO bloqueó al proceso.
- **Preparado (o Bloqueado) -> Finalizado**: terminación de un proceso por parte de otro (en la mayoría de los SO modernos, no se permite. En modo super usuario sí se puede).


## 2. DESCRIPCIÓN Y CONTROL DE PROCESOS
### 2.1 Descripción de procesos: PCB
>> carr pag .87 y p.137
- punteros de pila: cuando se ejecutan funciones

diferencia entre un apila: el primero que se atiende el último que ha llegado
cola: se atiende el primero que ha llegado

En las funcines cuando se va acumulando se forma nuevo **registro de activación** donde están los datos, se guarda la dirección en una pila, tiene una dirección que es lo que se conoce como puntero de pila, que soluciona todos estos problemas.

#### Creación de un proceso: Inicialización de PCB
Una vez que el SO decide crear un proceso procederá de la siguiente manera:
1. **Asignar un identificador de proceso único al proceso**: se añade una nueva entrada a la tabla primaria de procesos, que contiene una entrada por proceso.
2. **Reservar espacio para proceso**: incluye todos los elementos de la imagen del proceso. Para ello, el SO debe conocer cuánta memoria se requiere para el espacio de direcciones privado (programas y datos) y para la pila de usaurio. Estos valores se pueden asignar por defecto basándonos en el tipo de proceso, o pueden fijarse en base a la solictud de creación del trabajo remitido por el usuario. Por último, se deb reservar el espacio para el BCP.
3. **Inicialización del BCP**: la parte de identificación de proceso del BCP contiene el identificador del proceso y otros identificadores (como el indicador del proceso padre). En la información de estado de proceso del BCP, que se inicializa con la mayoría de entradas a 0, excepto el contador de programa (fijado en el punto entrada del programa) y los punteros de pila de sistema (fijados para definir los límites de la pila del proceso). La parte de información de control de procesos se inicializa en base a valores por omisión, considerando también los atributos que han sido solicitados para este proceso. La prioridad se puede fijar y el proceso no debe poseer ningún recurso (dispositivos de E/S, ficheros) a menos que exista una indicación explícita o que hayan sido heredados del padre.
4. **Establecer los enlaces apropiados**: si el SO mantiene cada cola del planificador como una lista enlazada, el nuevo proceso debe situarse en la cola de Listos o en Listos/Suspendidos.
5. **Creación o expansión de otras estructuras de datos**: el SO puede mantener un registro de auditoría por cada proceso que se puede utilizar posteriormente a efectos de facturación y/o de análisis de rendimiento de sistema.

En resumen:
1. Asignar identificador único al proceso.
2. Asignar un nuevo PCB.
3. Asignar memoria para el programa asociado.
4. Inicializar PCB:
	4.1 PC: dirección inicial de comienzo del programa.
	4.2 SP: dirección de la pila de sistema.
	4.3 Memoria donde reside el programa.
	4.4 El resto de campos se inicializan a valores por omisión.

### 2.2 Control de procesos
#### 2.2.1 Modo de ejecución del procesador

- **Modo usuario**: no accede a todos los registro de memoria, contador de programa, o registro de instrucción, tampoco otras instrucciones  
- **Modo núcleo, kernel, supervisor o sistema**: para pasar de uno a otro, se detecta que hay una operación que no se puede hacer en modo usuario.

##### ¿Cómo utiliza el SO el modo de ejecución?
El modo de ejecución (incluido en PSW) cambia a modo kernel,
automáticamente por hardware, cuando se produce:
	- Una **interrupción**: se compara la prioridad.
	- Una **excepción**: algo que no debería ocurrir pero ocurre, "overfloat" se levanta una alerta entra el SO, si lo que pasa no tiene riesgo para el resto de los procesos se deja pasar (depende del compilador), otra que ocurre se lee de un fichero, se acaba y se pide que sigue leeye, s en  este caso se aborta el programa.
	- Una **llamada al sistema**: leer disco, C pone un código que supone una rutina del SO. Llamo al sistema, se lee el dato que quiero, se manda interrupción, en el ciclo de instrucción mira a ver si era la siguiente.

Seguidamente se ejecuta la rutina del SO correspondiente al evento producido.
Finalmente, cuando termina la rutina, el hardware restaura automáticamente el modo de ejecución a modo usuario.

#### 2.2.2 Operación de cambio de modo
En la fase de interrupción, el procesador comprueba que no exista ninguna interrupción pendiente. Si no hay interrupciones pendientes, el procesador pasa a la fase de búsqueda de instrucción, siguiendo con el programa del proceso actual. Si hay una interrupción pendiente, el proceso actúa así:
1. Coloca el contador de programa en la dirección de comienzo de la rutina del programa manejador de la interrupción.
2. Cambia de modo usuario a modo núclero de forma que el código de tratamiento de la interrupción pueda incluir instrucciones privilegiadas.<br>
	
	El procesador pasa a la fase de búsqueda de instrucción y busca la primera instrucción del programa de manejo de interrupción, que le dará servicio. El contexto del proceso que se ha interrumpido se salvaguarda en el BCP del programa interrumpido.<br>
	Es decir, se ejecuta una rutina del SO en el contexto del proceso que se encuentra en estado "Ejecutándose".<br>
	La operación de cambio de modo se puede realizar siempreque el SO pueda ejecutarse, luego como resultado de una interrupción, excepción o llamada al sistema.
	

#### 2.2.3 Pasos en la operación de cambio de usuario a kernel
1. El que detecta el cambio de modo es el hardware, cuando el compilador detecta una llamada al sistema, interrucpción o excepción. El hardware salva cel contador de programa (**PC**) y la palabra de estado del proceso (**PSW**) y cambia el bit de modo a **modo kernel**.

2. Se determina automáticamente la **rutina del SO** que deb ejecutarse y cargar el **PC** con su dirección de comienzo.

3. **Ejecutar la rutina**. Posiblemente la rutina comience **salvando** el resto de registros del procesador y termine **restaurando** en el procesador la información de registros previamente salvada.

4. Volver de la **rutina del SO** al proceso que se estaba ejecutando. El **hardware** automáticamente restaura en el procesador la información del **PC** y **PSW** previamente salvada.

#### 2.2.4 Operación de cambio de contexto (cambio de proceso)
Un cambio de modo puede ocurrir sin que se cambie el estado del proceso actualmente en estado Ejecutando. Salvaguarda del estado y su posterior restauración comportan solo una ligera sobrecarga. Sin embargo, si el proceso actualmente en estado Ejecutando, se va a mover a cuqluier otro estado, entonces el SO debe realizar cambios sustanciales en su entorno. Los pasos a realizar para cambiar de proceso son:
1. Salvar el estado del procesador, incluyendo el contador de programa y otros registros.
2. Actualizar el BCP que está en el estado Ejecutando (incluye cambiar el estado del proceso a otro estado). También se tienen que actualizar otros campos importantes, incluyendo la razón por la cual el proceso ha dejado el estado de Ejecutando y demás información de auditoría.
3. Mover el BCP a la cola apropiada (Listo, Bloqueado en el evento i, Listo/Suspendido).
4. Selección de un nuevo proceso a ejecutar.
5. Actualizar el BCP elegido (incluye pasarlo al estado Ejecutando).
6. Actualizar las estructuras de datos de gestión de memoria.
7. Restaurar el estado del procesador al que tenía en el moento en el que el proceso seleccionado salió del estado Ejecutando por última vez, leyendo los valores anteriores de contado de programa y registros. <br>
	Por tando, el cambio de proceso, que implica un cambio en el estado, requiere un mayor esfuerzo que un cambio de modo.
	Se puede realizar cuando el SO pueda ejecutarse y decida llevarlo acabo. Luego solamente como resultado de una interrupción, excepción o llamada al sistema.

#### 2.2.5 Pasos en una operación de cambio de contexto (Dispatcher)
1. Salvar los registros del procesador en el **PCB** del proceso que actualmente está en estado "**Ejecutándose**".
2. **Actualizar** el campo **estado del proceso** al nuevo estado al que pasa e insertar el **PCB** en la **cola** correspondiente.
3. Seleccionar un **nuevo proceso del conjunto** de los que se encuentran en estado "**Preparado**" (Scheduler o Planificador de CPU).
4. **Actualizar el estado del proceso** seleccionado a "**Ejecutándose**" y sacarlo de la cola de preparados.
5. **Cargar los registros** del procesador con la información de los registros almacenada en el **PCB del proceso** seleccionado.


- ¿Si se produce una interrupción, una excepción o una llamada al sistema, se produce necesariamente un cambio de modo? ¿y un cambio de contexto?


## 3. HEBRAS (hilos)
### 3.1 Concepto de Hebra (hilos)
El concepto de **proceso (tarea)** tiene dos características diferenciadas e independientes que permiten al SO:
- **Propiedad de recursos:** controla la asignación de los recursos necesarios para la ejecución de programas.


- **Planificación/ejecución:** la ejecuicón de un proceso sigue una ruta de ejecución (traza) a través de uno o más programas. Esta ejecución puede estar intercalada con ese u otros procesos. Por lo que un proceso tien un estado de ejecución (Ejecutando, Listo...) y una prioridad de activación y esta es la que se planifica y activa por el SO.<br>
Para distinguir estas características, la unidad que se activa se denomina **hilo (thread), o proceso ligero**, mientras que la unidad de propiedad de recursos se denomina **proceso o tarea**.<br>
>Proceso: programa más lo que necesita, la unidad de procesamiento, lo que el SO le asigna los recursos que necesite,
puede ocurrir (cada sistm hace los que le sale de las narices). Por ejemplo se está navegando, se abren ventana, procesos distintos, tenemos instrucciones y datos, el proceso es el mismo, lo que cambia son los datos , en vez de abrir procesos nuevos, se abren hebras, proceso el mismo, datos de cada hebra distinto, deteo del bloque de conrtol de proceos se parten nuevos registos, direcciones, se ahorra mucha memoria de instrucciones.
>navegado -> proceso asociado a ese programa, dentro de la misma ejecucion (navegador) se abre una hebra. Hebra ejecución independiente del mismo proceso.
>Proceso unidad de gestión de un programa al que se asocian memeoria y gestión, si el codigo es el mismo en una hebra te ahorras el código en memoria, la hebra se paraleliza la ejecución del programa, el mismo código de programa abre las ejecuciones paralelas, así el programa avanza más rápido, hasta sincronizarse esto son hebras de un mismo proceso.
>Ejemplo el servidor, hay un progrma que continuamente está leyendo el puerto, cuando detecta ue hay una entrada habre un hebra para atencdeae al programa.
>Esto se utilizar para acelerar programas, sobretodo programas de cálculo mostruosos, ventajas de la hebras, se consume menos memoria, lo estados de las hebras son los mismos que los de los precesos.
<br>
**Multihilo** se refiere a la capacidad de un SO de dar soporte a múltiples hilos de ejecución en un solo proceso. Y el enfoque tradicional de un solo hilo de ejecución por proceso, en el que no se identifica con el concepto de hilo es el **monohilo**.<br>
En un entorno multihilo, un proceso se define como la unidad de asignación de recursos y una unidad de protección. Características:
- La **tarea** se encarga de soportar todos los recursos necesarios (incluida la memoria).
- Cada una de las hebras permite la **ejecución del programa** de forma independiente del resto de hebras.

#### 3.2 Modelo de cinco estados para hebras
Las hebras hebras debido a su característica de ejecución de programas presentan cinco estados análogos al modelo de estados para procesos:
- Ejecutándose
- Preparado (listo para ejecutarse)
- Bloqueado
- Nuevo
- Finalizado
<img src="media/tema2/diap30.png">

#### 3.3 Ventajas de las hebras
Los mayores beneficios de los hilos provienen de las consecuencias del rendimiento:
1. Menor tiempo de **creación** de una hebra en un proceso ya creado que la creación de un nuevo proceso.
2. Menor tiempo de **finalización** de una hebra que de un proceso.
3. Menor tiempo de **cambio de contexto (hebra)** entre hebras pertenecientes al mismo proceso.
4. Facilitan la **comunicación** entre hebras pertenecientes al mismo proceso.
5. Permiten aprovechar las **técnicas** de programación concurrente y el multiprocesamiento simétrico.

## 4. GESTIÓN BÁSICA DE MEMORIA
### 4.1 Carga absoluta y reubicación
Los requisitos que la gestión de memoria debe satisfacer son:
- Reubicación.
- Protección.
- Compartición.
- Organización lógica.
- Organización física.
<br>
**REUBICACIÓN**
Es la capacidad de cargar y ejecutar un programa en un lugar arbitrario de la memoria. <br>
En un sistema multiprogramado, la memoria principal disponible se comparte entre varios procesos. Por lo que no es posible saber anticipadamente qué programas residirán en memoria principal en tiempo de ejecución de su programa. Sería bueno poder intercambiar procesos en la memoria principal para maximizar la utilización del procesador, proporcionando un gran número de procesos para la ejecución. Una vez que un programa se ha llevado al disco, sería bastante limitante tener que colocarlo en la misma región de memoria principal donde se hallaba, cuando este se trae de nuevo a la memoria. Por el contrario, podría ser necesario **reubicar** el proceso a un área de memoria diferente. <br>
Por tanto, no se puede conocer de forma anticipada dónde se va a colocar un programa y se debe permitir que los programas se puedan mover en la memoria principal, debido al *intercambio o swap*. Esto pone de manifiesto a aspectos técnicos relacionados con el direccionamiento.<br>
Las instrucciones de salto contienen una dirección para referenciar una instrucción que se va a ejecutar a continuación. Las instrucciones de referencia de los datos contienen la dirección del byte o palabra de datos referenciados.<br>

**CARGA**
El primer paso en la creación de un proceso activo es cargar un programa en memoria principal y crear una imagen del proceso. En la carga de programa se debe satisfacer el direccionamiento siguiendo tres técnicas diferentes:
- Carga absoluta.
- Carga reubicable.
- Carga dinámica en tiempo real.
<br>
**Carga absoluta**
Consiste ne asignar direcciones físicas (direcciones de memoria principal) al programa en tiempo de compilación. El programa no es reubicable. <br>
Un cargador absoluto requiere que un módulo de carga dado deb cargarse siempre en la misma ubicación de la memoria principal. Por tanto, en el módulo de carga presentado al cargador, todas las referencias a direcciones deben ser direcciones de memoria principal específicas o absolutas. <br>
Es preferible permitir que las referencias de memoria dentro de los programas se expresen simbólicamente, y entonces resolver dichas referencias simbólicas en tiempo de compilación o ensamblado. Cada referencia a una instrucción o elemento de datos se representa inicialmente como un símbolo. A la hora de preparar el módulo para su entrada a un cargador absoluto, el ensamblador o compilador convertirá todas estas referencias a direcciones específicas. <br>
<br>
<br>
No es posible conocer previamente las direcciones de memoria de un programa, el SO es el que se encarga de posicionar y tener la información de la memoria.<br>
Las direcciones que puede asignar un compilador son las físicas o absolutas y las que empiezan en cero, realticas o lógicas, utilizar siempre absolutas implicaría que siempre se utilizase la misma direcciones de memoria, en el caso de instrucciones se suma lo mismo o en el caso de bucles también se saltas. 
<br>
<img src="media/tema2/carga_absoluta_reubicacion.png" width="600" height="350"> 
<br>
Cuando se compila un programa se realiza la reubicación, a la carga relativa se el suma la dirección inicial en la que se inicia.
(en el núcleo, el esto tiene direccione es carga absoluta, en el se basa el grub)
si la máquina que tienes no tiene la memoria suficiente, ejecutar los mismos programas comparando con una de mauor, lo que tiene poca memoria, lo que tiene que hacer es coger y descargar los procesos de discos, la localización supone supa cálculo...

La direcciones lógicas se combierten en físicas después de la de compilación y antes de la ejecución o antes de que use la dirección, estos dos momentos son estáticas y dinámica.

### 4.2 Reubicacion estática
El **compilador** genera **direcciones lógicas** (relativas) de 0 a M. La decisión de **dónde ubicar** el programa en memoria principal se realiza en **tiempo de carga**. El **cargador** añade la dirección base de carga a todas las referencias relativas a meomria de programa.<br>
Es decir, una vez que se conoce la posición de memoria en la que se va a colocar el programa, durante la carga a cada dirección de memoria lógica le suma la dirección base, la primera dirección donde se va a cargar, dando lugar a direcciones absolutas.<br>
La **ventaja** que aporta es que el cambio de dirección lógica a absoluta solo se hace una vez, pero como **desventaja** ya no se puede <img src="media/tema2/diap35.png">

### 4.3 Reubicación dinámica
El **compilador** genera **direcciones lógicas** (relativas) de 0 a M. La **traducción** de direcciones lógicas a físicas se realizan en **tiempo de ejecución**, luego el programa está cargado con referencias relativas. Además, requiere apoyo **hardware**. <br>
Es decir, durante la carga se escribe en memoria principal las direcciones lógicas o relativas y cada vez que se vaya a acceder a una de estas direcciones se le suma la dirección base.<br>
Esto tiene de **ventaja** el ahorro de operaciones en caso de qeu haya direcciones que no se utilicen, aunque en la actualidad la reubicación absoluta es obsoleta ya que ahora se encarga la CPU de esto.
<img src="media/tema2/diap36.png">

### 4.4 Espacios para las direcciones de memoria

#### Espacio de direcciones lógico.
Conjunto de direcciones lógicas (o relativas) que utiliza un programa ejecutable.

#### Espacio de direcciones físico.
Conjunto de direcciones físicas (memoria principal) correspondientes a las direcciones lógicas del programa en un instante dado. El sistema operativo contiene un mapa con la memoria, procesos, tabla de signos...  Cuando se está realizando la compilación a cada nombre se el asigna una dirección de memoria, para los símbolos no resueltos por el compilador ( ejemplo funciones externas) se resuelven durante la encadernación o enlace. <br>
> Como apuntes: la tabla de símbolos puede ser dinámica o estática, en caso de ser dinámica el encuadernador hará uso de ella.
<br>
> Los datos a los que se le asigna un valor al comienzo del programa, en memoria estarían despuén del código, en argumentos de programa y pila.
<br>
> Las pilas se van formando cada vez que se llama a una función, creando zonas de **registros de activación** que contienen los valores que van tomando las funciones.
<br>
> Para buscar una variable se buscan en los registros que la han llamado, a diferencia de la variables globales.
<br>
> Lo que se guarda en una pila de la CPU es la dirección de la dirección que es distinta a la pila de proceso, que está en la pila de la CPU y otra en memoria principal, en el registro de acivación de la variables globales.
<br>

<br>
**Montículo o módulo:** en él se van almacenando las variables dinámicas, las listas y las pilas, al final del espacio de memoria reservado. Para evitar un desbordamiento del montículo se uiliza el **recolector de basura** compacta el espacio no utilizado en memoria.

#### Mapa de memoria de un ordenador.
Todo el espacio de memoria direccionable por el ordenador. Normalmente depende del tamaño del bus de direcciones.
#### Mapa de memoria de un proceso.
Se almacena en una estructura de datos (que reside en memoria) donde se guarda el tamaño total del espacio de direcciones lógico y la correspondencia entre las direcciones lógicas y las físicas.
<img src="media/tema2/mapa_de_memoria.png">


### 4.5 Problema de la fragmentación de memoria
Con particiones del mismo tamaño, la ubicación de los procesos en memoria es trivial. En cuanto haya una partición disponible, un proceso se carga en dicha partición. Si todas las particiones se encuentran ocupadas por procesos que no están listos para ejecutar, entonces uno de dichos procesos debe llevarse a disco para dejar espacio para un nuevo proceso. Cuál de los procesos se lleva a disco es una decisión de **planificación**. <br>
Con particiones de diferente tamaño, hay dos formas posibles de asignar los procesos a las particiones. La forma más sencilla consiste en asignar cada proceso a la partición más pequeña dentro de la cual cabe. Se necesita una cola de planificación para cada partición que mantenga procesos en disco destinados a dicha partición. La ventaja es que los procesos siempre se asignan de tal forma que se minimiza la memoria malgastada dentro de una partición (fragmentación interna). Pero no es óptima. Una técnica óptima sería emplear una única cola para todos los procesos. En el moento de cargar un proceso en la memoria principal, se selecciona la partición más pequeña disponible que puede albergar dicho proceso. Si todas las particiones están ocupadas, se debe llevar a cabo una decisión para enviar a *swap* a algún proceso. <br>
El uso de particiones de distinto tamaño proporciona un grado de flexibilidad frente a las particiones fijas. Además, los esquemas de particiones fijas son relativamente sencillos y requieren un soporte mínimo por parte del SO y una sobrecarga de procesamiento mínimo. Sin embargo, tiene una serie de **desventajas**:
- El número de particiones especificadas en tiempo de generación del sistema limita el número de procesos activos (no suspendidos) del sistema.
- Debido a que los tamaños de las particiones son preestablecidos en tiempo de generación del sistema, los trabjaos pequeños no utilizan el espacio de las particiones eficientemente. En un entorno donde el requisito de almacenamiento principal de todos los trabajos se conoce de antemano. Se trata de una técnica ineficiente.<br>

<img src="media/tema2/problemas_fragmentacion_memoria.png">
<br>


### 4.6 Solución a la fragmentación de memoria
Con el particionamiento dinámico, las particiones son de longitud y número variable. Cuando se lleva un proceso a la memoria principal, se le asgina exactamente tanta memoria como requiera y no más. <br>
Es decir, la solución es trocear el espacio lógico en unidades más pequeñas: **páginas** (elementos de longitud física), o **segmentos** (elementos de longitud variable). Los trozos no tienen por qué ubicarse consecutivamente en el espacio físico.<br>
Los esquemas de organización del espacio lógico de direcciones y de traducción de una dirección del espacio lógico al espacio físico son:
- Paginación
- Segmentación
<br>
Por lo que, para solucionar ese problema, está el Buffer de traducción adelantada TLB, lo que se tiene en CPU, es un trocito de la tablas de página en marcos, se lee ese trocito, si aparece el marco, solo habría un acceso, si no se esta memoria se llama Caché (memoria muy rápida).  La forma de acceder pro ardware, inteneta buscar esa página el paralelo, esta tabla tiene número pagin num marco y bits de protección, en cache no necesita el número de páginas


#### 4.6.1 Paginación
Consiste en trocear los procesos de manera homogénea, es decir, todo se parte de la misma manera: la memoria física se divide en bloques iguales, el tamaño es potencia de dos, de 512 B a 8 KB estas porciones se denominan **marcos de página**.<br>
El espacio lógico de un proceso se divide conceptualmente en bloques del mismo tamaño, salvo el último que puede ser más pequeño, denominados **páginas**. <br>
Los marcos de página contendrán páginas de los procesos. <br>
Normalmente en la paginación por una parte va el código y por otra los datos, cuando se ejecuta el proceso los marcos libres empiezan a ocuparse, no necesariamente de manera ordenada. El estado de un marco se recoge en el **mapa de marcos libres**.
Para acceder a una dirección, se debe saber la página en que está, y dentro de la página el desplazamiento,es decir, desde el principio de su ejeción necesito saber en qué marco se está desarrollando y línea concreta.<br>
<img src="media/tema2/direcciones_paginacion.png">
<br>
Cuando la CPU genere una dirección lógica será necesario traducirla a la dirección física correspondiente, la **tabla de páginas** mantiene información necesaria para realizar dicha traducción. Existe una tabla de páginas por proceso.
**Tabla de marcos de página**, usada por el SO y contiene información sobre cada marco de página.

##### 4.6.1.1 Contenido de la tabla de páginas
Una entrada por cada página del proceso:
- **Número de marco** en el que está almacenada la página si está en MP.
- **Modo de acceso** autorizado a la página (bits de protección).
##### 4.6.1.2 Esquema de traducción
<img src="media/tema2/esquema_traduccion_paginacion.png">

##### 4.6.1.3 Implementación de la Tabla de Páginas
- La tabla de páginas se mantiene en memoria principal.
- El *registro base de la tabla de páginas* (**RBTP**) apunta a la tabla de páginas (suele almacenarse en el PCB del proceso).
- En este este esquema cada acceso a una instrucción o dato requiere dos accesos a memoria, uno a la tabla de páginas y otro a memoria.
##### 4.6.1.4 Búfer de Traducción Adelantada (TLB)
Toda referencia a la memoria virtual puede causar dos accesos a la memoria física: uno para buscar la entrada la tabla de páginas apropiada y otro para buscar los datos solicitados. De esa forma, un esquema de memoria virtual básico causaría el efecto de duplicar el tiempo de acceso a memoria. Para solventar este problema, la mayoría de esquemas de la memoria virtual utilizan un *cache* especial de alta velocidad para las entradas de la tabla de página (**TLB**, Translation Look-aside- Buffer). Esta *cache* funciona de forma similar a una memoria cache general y contiene aquellas entradas de la tabla de páginas que han sido usadas de forma más reciente. La organización del hardware de paginación resultante es:
<img src="media/tema2/diap48.png">

<br>
Dada una dirección virtual, el procesador primero examina la TLB, si la entrada de la tabla de páginas solicitad está presente (acierto en TLB), entonces se recupera el número de marco y se construye la dirección real. Si la entrada de la tabla de páginas solictiada no se encuentra (fallo en la TLB), el procesador utiliza el número de página para indexar la tabla de páginas del proceso y examinar la correspondiente entrada de la tabla de páginas. Si el bit de presente está puesto a 1, entonces la página se encuentra en memoria principal, y el procesador puede recuperar el número de marco desde la entrada de la tabla de páginas para construir la dirección real. El procesador también autorizará la TLB para incluir esta nueva entrada de tabla de páginas. Finalmente, si el bit presente no está pueso a 1, entonces la página solicitad no se encuentra en la memoria principal y se produce un fallo de acceso de meomria, llamado **fallo de página**. En este punto, abandonamos el dominio del hardware para invocar al SO, el cual cargará la página necesaria y actualizada de la tabla de páginas.
<br>
Cada entrada de la TLB debe incluir un número de página así como la entrada de la tabla de páginas completa. El procesador proporciona un hardware que permite consultar simultáneamente varias entradas para determinar si hay una conciencia sobre un número de página. Esta técnica se denomina **resolución asociativa (asociative mapping)** que contrasta con la resolución directa, o indexación, utilizada para buscar en la tabla de páginas. El mecanismo de memoria virtual debe interactuar con el sistema de cache (no la cache de TLB, sino la cache de la memoria principal).
<br>
En resumen, el problema de los dos accesos a memoria se resuelve con una caché hardware de consulta rápida denominada búfer de traducción
adelantada o **TLB** (*Translation Look-aside Buffer*).
<br>
El TLB se implementa como un conjunto de **registros asociativos** que permiten una búsqueda en paralelo. De esta forma, para traducir una dirección:
1 Si existe ya en el registro asociativo, obtenemos el marco.
2 Si no, la buscamos en la tabla de páginas y se actualiza el TLB con esta nueva entrada.

##### 4.6.1.5 Ventajas y desventajas
- **Ventaja**: se gestiona mejor la memoria.
- **Desvetanjas**: los accesos a memoria, sin fragmentación son más rápidos, de la otra manera hay que hacer varios accesos, registros
1. cpu memoria principas--> lee marco
2. memoria al marco 25 --> coge desplazamineto
En total hace dos accesos a memoria.

#### 4.6.2 Segmentación
Esquema de organización de memoria que soporta mejor la visión de memoria del usuario: un programa es una colección de unidades lógicas (segmentos). Por ejemplo: procedimientos, funciones, pila, tabla de símbolos, matrices, etc.<br>
<img src="media/tema2/diap49.png">
<br>

>>Esto que es??? -------> Divide el programa en trozos no necesariamente iguales, relacionados con la arquitectura del programa.
En las direcciones lógicas de la paginación se deberá de dar la página y  el desplazamiento para poder ser traducidas a direcciones físicas, para ello el SO crea una tabla de paginas (*entradas*) y en cada fila aparece el **marco** en el que está la página y  bits de protección o **modo de acceso**, de lectura o escritura. La tabla de páginas está en memoria principal, por tanto la tabla empezará a partir de una determinada dirección base, esa dirección base, cuando se ejecuta el proceso se carga en el registro base de la tabla de páginas, (el desplazamiento es el mismo dentro y fuera de la máquina).

##### 4.6.2.1 Tabla de Segmentos
Una dirección lógica es una tupla:
 <número_de_segmento, desplazamiento>
La **Tabla de Segmentos** aplica *direcciones bidimensionales* definidas por el usuario en direcciones físicas de una dimensión. Cada entrada de la tabla tiene los siguientes elementos (aparte de presencia, modificación y protección):
- **base**: dirección física donde reside el inicio del segmento en memoria.
- **tamaño**: longitud del segmento.
##### 4.6.2.2 Implementación de la Tabla de Segmentos
La tabla de segmentos se mantiene en memoria principal.
- El **Registro Base de la Tabla de Segmentos (RBTS)** apunta a la
tabla de segmentos (suele almacenarse en el PCB del proceso).
- El **Registro Longitud de la Tabla de Segmentos (STLR)** indica el
número de segmentos del proceso; el no de segmento s, generado
en una dirección lógica, es legal si **s < STLR** (suele almacenarse
en el PCB del proceso).
##### 4.6.2.3 Esquema de traducción
> Insertar diapositiva 52

## 5. COMPILADORES

Ejemplo de sentencia de un programa a1 = b + c + 13. 77
El compilador lee de izquierda a derecha e intenta identificar cada elemento, construyendo
una **tabla de símbolos**.

Signo |  Datos |  Dirección memoria asociada
------| ------ | -----------------------------
a1    |   666  |   0xab0f20x53 (En hexadecimal)


De esta manera, cada vez que se haga referencia a *a* se redirecciona a la dirección asignada por el compilador.

En los primeros compiladores el número de direcciones era menor y se podía hablar de dirección de memoria absoluta. Sin embargo, en la actualidad, a alto nivel, el uso de direcciones es más complejo, abarcando incluso direcciones de direcciones, como es el caso de de las sentencias de control (if, while...).
Para facilitar el trabajo se hacen asignaciones de **memoria relativa** en lo que respecta a la zona de memoria que se le otorga.  Estas direcciones
relativas comienzan en 0 y continuan dependiendo del tamaño en bytes del tipo
de dato almacenado. 

Los pasos que comprenden un programa antes de ser ejecutado son: compilación,encuadernación y la formación del ejecutable:

- Durante la carga del programa, se lee del disco y se copia esa información en memoria principal por el SO. El SO contiene un *mapa* con las direcciones relativas de memoria. Estas se suman a la llamada **dirección base**, para obtener las direcciones reales (cada vez que se quiera acceder a una variable durante la ejecución).

El SO también protege sobre problemas del programa. Por ejemplo, el acceso a los dispositivos lo hacen rutinas del SO, que comprueban si la dirección de memoria a la que accede el programa es correcta. En caso contrario, el SO se encargar de abortar el programa.

Volviendo a cómo se almacenan la variables, en lo concerniente a las constantes, estas se tratan exactamente igual que las simbólicas, con la única diferencia que como identificador, el nombre de la variable es el propio símbolo, el resto es lo mismo, como valor se guarda a ellos y tiene también una dirección de memoria asociada.

  - **Punteros**: Es una variable que almacena una dirección de memoria.  Son la base de las estructuras dinámicas de datos. El riesgo de su uso radica en la posibilidad de sobreescribir los datos de la memoria por error.

  - **Arrays**: son realmente punteros encadenados en bloques de memoria. Así, es posible recorrer el *array* mediante aritmética de punteros, es decir,aumentando en 1 la dirección de memoria asociada.

  - Existen dos formas de pasar argumentos a una función:

    - *Por valor*: en la función se trabaja sobre una copia del valor pasado. Se puede considerar más seguro ya que un cambio en la variable dentro de la función no influye de ninguna forma al valor original.

    - *Por referencia:* a la función se le pasa la dirección de memoria de una variable. Por tanto, la función puede modifica el valor original, lo que constituye un riesgo en caso de error.

> En el caso de C++ existen dos subtipos de paso de referencias: por punteros, o por referencias. El paso por punteros es heredado de C, mientras que las referencias son específicas de C++, y facilitan el paso de referencias evitando errores debidos al trabajo con punteros.

### 5.1 Resumen

El compilador conforme traduce, asigna direcciones relativas a variables y controladores de flujo. Cuando el programa se carga en memoria el SO es el encargado de gestionar el acceso del programa en memoria.
<br>
