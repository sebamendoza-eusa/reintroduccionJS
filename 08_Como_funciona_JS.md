# Como funciona JavaScript: la pila de llamadas, *event loop*, cola de tareas...

**Para entender JavaScript hay que tener en cuenta que es un lenguaje interpretado**. Esto quiere decir que el código, al ejecutarse, va a ir leyéndose línea por línea y ejecutándose paso a paso.

A lo anterior se le une que JavaScript es **un lenguaje de programación de un solo hilo** (*single thread*), lo que quiere decir que sólo puede ejecutar una instrucción en cada paso del programa. El principal problema que puedes encontrar con esto es que el programa, al ejecutar sus instrucciones, se bloquee en su único hilo, y que ello se traduzca en que el navegador también se bloquee, se ralentice, e incluso que en ocasiones no pueda ejecutar ninguna acción.

Para entender este mecanismo hay que, a su vez, comprender otros conceptos importantes relacionados con el funcionamiento interno de JavaScript, como son la **pila de llamadas** (*call stack*), el **bucle de eventos** (*event loop*) o la **cola de tareas** (*task queue*). Sin embargo, quizás sea interesante parar un momento en un elemento fundamental sin cuyo concurso sería imposible que JavaScript funcionase: **El motor de JS** (*JavaScript Engine*)

## El motor de JavaScript

Un motor es un programa que se encarga de convertir código de alto nivel (JavaScript, Python o C, por ejemplo) en código de bajo nivel (Machine Code o Bytecode, por ejemplo).

En el caso de JavaScript, cada navegador incorpora su propio motor que interpreta el lenguaje y compila el programa. Los más habituales son:

- V8 Engine (Google Chrome), el cual también es motor de Node.js
- Spider Monkey (Mozilla Firefox)
- Chakra (Microsoft Edge)
- JavaScriptCore (Apple Safari)

Quizás el más importante de todos sea V8 por su extensión a través de Chrome y porque forma parte del núcleo de NodeJS.

### Pero ¿cómo funciona?

Para ejecutar un programa en cualquier lenguaje, hay que convertirlo en instrucciones que las computadoras puedan entender, es decir, a **código máquina**.

Los lenguajes compilados transforman todo el código **antes de ejecutarlo**, por lo que pueden hacer optimizaciones generales para que el programa sea más eficiente.

Para que el programa compile tiene que estar libre de errores. Generalmente esa compilación lleva un poco de tiempo, que va creciendo dependiendo del tamaño y complejidad del programa. Los programas compilados pueden ser más eficientes en ejecución, pero **cuesta más empezarlos a ejecutar.**

Por su parte, los lenguajes interpretados van ejecutando **línea por línea**, sentencia por sentencia. Por esto mismo no pueden hacer optimizaciones generales, pero es más fácil y rápido para el programador *empezar* a ejecutarlos. Normalmente tienen un **REPL** (Read - Eval - Print - Loop) que puede servir para jugar con ellos y hacer pruebas.

Se pude pensar que es *más fácil* desarrollar en lenguajes interpretados que compilados, por lo que su desarrollo es *más rápido*. Pero como los lenguajes compilados pueden hacer optimizaciones generales, son **más eficientes**.

Sin embargo, hoy en día,  JavaScript ya ha dejado de de ser un lenguaje *puramente interpretado* para convertirse en un lenguaje híbrido, con interpretación y compilado JIT *(Just In Time)*. Se comporta como interpretado cuando un programador lo corre, pero el motor compila el código, produciendo algunas veces un producto intermedio (*bytecode*) que puede ser optimizado para que las siguientes ejecuciones sean mucho más rápidas.

Las etapas por las que pasa el código en el motor JavaScript podrían resumirse a continuación:

1. **Escaneo**. Convierte el texto del código que escribes en *tokens*. Un token es un bloque de carácteres que tienen un significado sintáctico.
2. **Parseo**. Se puede entender como la ‘lectura’ de un texto para transformarlo en una estructura de datos. En esta fase se convierte el conjunto de *tokens* generados en la fase anterior en una estructura sintáctica denominada AST.
3. **Interpretación**. En esta fase se toma el AST y se convierte en una primera versión de código que la máquina ya puede ejecutar, *sin optimizaciones*. Genera además código intermedio (bytecode) que puede ser pasado a la siguiente etapa para optimizarlo.
4. **Optimización**. Esta parte es ejecutada por un compilador JIT, que analiza el código, cómo se comporta, los tipos de datos usados para crear una versión más optimizada en código máquina. Si las optimizaciones fallan, el bytecode sigue siendo ejecutado por el intérprete.

Las últimas dos etapas son donde el código se ejecuta, una en forma de bytecode interpretado y la otra en forma de código máquina **altamente eficiente y optimizado**.

### El tiempo de ejecución

Durante la ejecución, el motor de JavaScript debe mantener por lo menos dos cosas:

1. La información sobre el programa
2. En qué parte del programa estamos

Esto lo hace mediante dos espacios de memoria organizados específicamente para estas tareas:

1. El **Heap** (*Montón*). Encargado de mantener la información de las variables y todo otro dato ocupado por el programa.
2. El **Stack** (*Pila*). Encargado de llevar un registro de las llamadas a funciones y contextos de ejecución.

Además necesitamos a alguien que libere memoria para que nuestro programa no crezca infinitamente en la memoria y el *heap* sea fácil de acceder. De ello se encarga el **garbage collector** o *recolector de basura*.

## La pila de llamadas

La **pila de llamadas** es el mecanismo mediante el que el intérprete de JavaScript hace el seguimiento de cómo se invocan múltiples funciones, qué función se esta ejecutando actualmente y qué funciones son llamadas desde esa función, etc.

Una pila de procesos es una estructura habitual en programación. Su particularidad reside en el hecho de que **el último proceso que entra en la pila es el primero en ejecutarse**. En inglés se asocia al acrónimo ***LIFO*** (*Last In First Out*)

Cuando se invoca a una función, un contexto de ejecución se coloca en la pila de ejecución.

El funcionamiento de la pila de ejecución en JavaScript se puede resumir en tres pasos principales:

1. Cuando se llama a una función, se crea un contexto de ejecución en forma de registro en la pila y se agrega a la parte superior dela misma
2. A medida que se ejecuta el programa, se llaman más funciones, se generan más contextos y se agregan más registros a la pila en un orden LIFO.
3. Cuando se completa el contexto de ejecución de una función, se elimina su registro correspondiente de la pila, y el flujo de ejecución regresa al punto indicado por el puntero de retorno.

Como se ve los principales elementos a tener en cuenta en el funcionamiento de la pila de ejecución son:

1. Una **estructura de datos LIFO** basada el principio Last In, First Out para agregar y eliminar registros.
2. Un **control del flujo de ejecución** que se encarga de llamar y completar funciones.
3. Un **puntero de retorno** que indica dónde debe continuar el programa después de que se complete una función.

### Gestión de errores y excepciones

En ocasiones puede encontrarse un error o una excepción en la ejecución de una función. En ese caso JavaScript utiliza la pila de llamadas para manejar el control del flujo del programa, haciendo que en lugar de continuar con la ejecución de la función actual, el programa salte a una función de manejo de errores. Si ello no fuese posible, el error se propagaría hacia arriba en la pila de llamadas hasta encontrar un controlador de errores que lo gestione o hasta que se vacíe la pila y el programa se detenga.

### Desbordamiento de la pila

Básicamente el error de desbordamiento de pila ocurre cuando la pila agota el espacio que se le ha asignado para controlar las llamadas a las funciones. Este agotamiento se produce habitualmente cuando se producen demasiadas llamadas a funciones sin que finalicen y puedan desalojarse. Este comportamiento está directamente relacionado en la mayoría de los casos con **llamadas a funciones recursivas**.

## Bucle de eventos *(event loop)*

El concepto de *bucle de eventos* es hasta cierto punto simple. El motor de JavaScript funciona en un ciclo infinito en el que espera por una tarea, luego ejecuta la tarea requerida y posteriormente vuelve a *dormir* a la espera de una nueva tarea.

¿Pero que pasaría si una tarea tarda mucho en ejecutarse? En principio la consecuencia sería que el bucle de eventos se bloquearía. Sin embargo, nuestra experiencia con JavaScript nos dice que eso no es así. Como siempre, con JS, las cosas no son exactamente como parecen.

Cuando intentamos entender el concepto de motor de JS (o RunTime) podemos estar pensando en un elemento aislado que ejecutar tareas en un único hilo. Sin embargo lo cierto es que el motor de JavaScript se encuentra insertado en un **entorno de ejecución** en el que también intervienen las **web APIs** del navegador.

Es aquí donde el bucle de eventos toma su verdadero significado. Para no bloquear el único hilo de tareas, aquellas que tienen una naturaleza asincrónica son derivadas desde el motor de JS a las web APIs, dejando la pila de llamadas libre para atender la siguiente tarea. Cuando el contexto de las funciones que están en las web APIs se completa estas no retornan directamente a la pila de tareas sino que quedan aparcadas en una estructura intermedia denominada ***Cola de callbacks*** donde permanecerán en espera. Es entonces cuando el bucle de eventos actuará, devolviendo a la pila de llamadas las  funciones callback de la cola **cuando aquella quede libre**

> Recomiendo la visualización del video de Philip Roberts: ¿Que diablos es el bucle de eventos? aquí: https://www.youtube.com/watch?v=8aGhZQkoFbQ
>
> Tendrás una visión muy aclaratoria de lo que has leído anteriormente.











 



