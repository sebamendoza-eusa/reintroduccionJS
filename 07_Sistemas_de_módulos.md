# Expresiones vs. declaraciones

La sintaxis de JS es el conjunto de reglas que definen cómo podemos combinar distintos símbolos para producir instrucciones válidas con el objeto de crear un script válido que el motor entienda.

En JS existen dos estructuras sintácticas importantes: las **expresiones**, que son fragmentos de código que producen un valor a ser evaluadas, y las **sentencias**, que son acciones que son ejecutadas para que nuestro script siga la lógica que queremos. 

Las expresiones son similares a las **palabras** en un idioma. Las expresiones pueden ser primarias, cuando se componen de una sola palabra  o complejas, cuando no es así.

Por ejemplo, la siguiente sería una expresión compleja, en la que se mezclan varios operadores y datos primarios 

```javascript
true && 2 * 9
```

Si entendemos que el estado de una variable es su valor actual, hay que tener en cuenta que **las expresiones no necesariamente cambian el estado de las variables**

```javascript
const a = 2;

a + 4 // expresion
console.log(a + 4) // 6
console.log(a) // 2, El valor de la variable (estado) no ha cambiado
```

Las **declaraciones (statements)** , a diferencia de las expresiones, **ejecutan acciones**. Podemos pensarlas como las oraciones en un idioma. Si en un idioma las oraciones terminan con un punto, en JS las sentencias se terminan con punto y coma, `;`

No pueden ser usadas como argumentos de funciones o en la parte derecha de una asignación o detrás de un operador. Hay varios tipos de sentencias en JS:

- Sentencias de expresión: No tienen mucho sentido si no buscamos su efecto secundario, que es asignar un valor a una variable o invocar el resultado de una función
- Sentencias vacías (muy raras de encontrar): Por ejemplo, un bucle `for` sin bloque asociado
- Sentencias de bloque: Muy habituales en el lenguaje. Los bloques de instrucciones se escriben entre llaves. Es muy recomendable, siempre que se pueda, usar este tipo de escritura de sentencias
- Sentencias de declaración: Declaran el valor de una variable. Un sentencia de declaración muy importante es la declaración de función. Se ampliará información más abajo.
- Sentencias de control: Son las que alteran el flujo normal de ejecución. Se incluyen aquí los bucles y los bloques condicionales. También las sentencias de salto, como `return`, `break`,  `continue` o `trow` estarían en este grupo.
-  Sentencias misceláneas: Se incluyen aquí aquellas sentencias que no pertenecen a cualquiera de los grupos anteriores. Ejemplo de estas sentencias podrían ser `debbuger` o `'use strict'`

## Declaraciones y expresiones en funciones

En JavaScript tenemos dos maneras principales de definir funciones, como una **declaración** o como una **expresión**.

Las funciones definidas de forma expresiva se sitúan a la derecha de un símbolo igual, asignándose su resultado a una variable. Una función declarada de forma expresiva puede llevar nombre o no, pero ese nombre sólo puede usarse en el scope de la propia función para ser llamada de forma recursiva. Las funciones expresivas que se definen sin nombre son denominadas funciones **anónimas**. Cuando definamos una función de forma declarativa, comenzaremos la instrucción con la palabra `function` y la acompañaremos del nombre y los parámetros de la misma. La declaración de función no puede hacerse nunca **de una función anónima**, bueno, salvo en un caso: la IIFE, en las que una función es declarada **e inmediatamente le pasamos los parámetros**...

Pero quizás es el **hoisting** la diferencia más importante entre las funciones definidas de forma declarativa y las definidas de forma expresiva. Cuando una función es definida de forma declarativa **es posible invocarla antes de definirla en el propio código**, ya que en tiempo de ejecución, el motor JS va a tener en cuenta todas las declaraciones de funciones antes de evaluarlas en expresiones. Sin embargo, **si la función en cuestión ha sido definida de forma expresiva, el hoisting no se aplica** (ni aunque la función expresiva no sea anónima). Es similar a invocar un objeto antes de crearlo: Esto es imposible en JS y provoca un error.

Un último detalle: Cuando definamos una función de forma declarativa no es necesario terminar el bloque de instrucciones con punto y coma, mientras que cuando estemos tratando con una función definida mediante expresión sí que debemos hacerlo. Es una buena práctica llevar a cabo estas reglas, aunque sabemos que el motor de JS en tiempo de ejecución lo va a hacer por nosotros.
