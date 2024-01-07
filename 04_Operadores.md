# Operadores básicos

Los operadores numéricos de JavaScript son `+`, `-`, `*`, `/` y `%` que es el operador de residuo o resto (o módulo). Los valores se asignan usando `=`, aunque también hay declaraciones de asignación compuestas, como `+=` y `-=`, Estas últimas equivalen a la expresión `x = x operador y`. Existe la posibilidad de usar  `++` y `--` para incrementar y disminuir respectivamente el valor de una variable. Además se pueden utilizar como operadores prefijos o sufijos.

Aunque los operadores anteriores son actúan entre valores numéricos, el operador `+` puede servir para concatenar cadenas de texto. Concatenar texto y números convierte a tipo `string` los números implicados. Cuidado con ello. De hecho, agregar una cadena vacía a cualquier valor lo convierte en tipo `string`

**Los operadores de comparación** son `<`, `>`, `<=` y `>=`. Estas funcionan tanto para cadenas como para números. La igualdad es un poco compleja. El operador doble-igual `==` realiza la coerción de tipos si se le pasan diferentes tipos. Si queremos evitar esto tendremos que usar el triple igual `===`. Los operadores  `!=` y `!==` comparan dos valores distintos.

> Para una referencia completa de todos los operadores usados en JS puedes consultar el siguiente enlace https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators

## Coerción de tipos en JS

Para entender el concepto de *coerción de tipos* hay que empezar por comprender qué es un lenguaje **fuertemente tipado**.

> Un lenguaje **fuertemente tipado** es aquel en el que cada tipo de datos está predefinido como parte del propio lenguaje y todas las constantes o variables definidas en un determinado programa han de estar descritas explícitamente con alguno de los tipos de datos permitidos.

JS es sin embargo un lenguaje **débilmente tipado**, lo que conlleva que no es necesario la declaración previa del tipo de una variable o constante. En JS la coerción se entiende como una conversión de tipos **en tiempo de ejecución** de aquellas constantes o variables que no han sido declaradas con alguno de los que son proporcionados por el lenguaje.

Así pues, la **coerción** es la conversión de valores de un tipo de dato a otro (Ejemplo: de cadena de texto a número). La coerción de tipos puede ser **explícita** o **implícita.** Es explícita si el proceso de coerción queda intencionalmente claro en el código. JS, al ser un lenguaje débilmente tipado, permite la posibilidad de la **coerción implícita de datos**, es decir una conversión automática en tiempo de ejecución. Esta coerción implícita ocurre cuando aplicamos un operador entre valores de diferentes tipos (con la única excepción del operador de comparación estricta `===`)

Vamos a ver algunas reglas que operan en la coerción implícita de datos:

- Sólo existen tres tipos de conversión automática: a `string`, a `boolean` o a `number`
- La conversión entre tipos primitivos opera de modo distinto a la conversión entre objetos
- Un `string` en una expresión que contiene números y alguno  de los operadores `-, *, /, %` se convierte a `number`
- El operador `+` puede operar de dos maneras: como concatenador de cadenas o como operador de suma matemática. Cuando con el operador `+` aparece un `string` actúa como concatenador, convirtiendo los tipos `number` en tipos `string`
- La conversión a `boolean` de los siguientes valores da como resultado un valor falso: `false, 0, null, undefined, "", NaN, -0`. Para el resto de valores la conversión a `boolean` proporciona un valor verdadero.

Si bien la coerción implícita está diseñada para ser de ayuda, ésta puede crear confusión si no se conocen en profundidad las reglas que rigen su comportamiento. La sensación común es que la coerción implícita es compleja y daña los programas con errores inesperados, por lo que en general debe evitarse.

## Comparadores `==` y `===`

JavaScript tiene dos maneras visualmente muy parecidas de comparar la similitud de dos valores, pero sin embargo funcionan de modo muy distinto. Nos referimos a los operadores de igualdad estricta `===` y de igualdad débil `==`. 

El operador `===` cuando compara valores primitivos nos dice **sin son del mismo tipo y si tienen el mismo valor**. Sin embargo al usar `==` obligamos al lenguaje **a hacer una coerción implícita de tipos** en caso de que ambos operandos no los tengan. El operador igualdad débil **necesita que los operandos sean del mismo tipo para completar la operación.**

Cuando usamos estos operadores con objetos, arrays o funciones, las cosas cambian un poco. Puede parecer extraño que objetos con las mismas propiedades y valores, al compararlos con estos operadores, den un valor `false`. Sin embargo este fenómeno se entiende perfectamente al recordar que cuando comparamos objetos, arrays o funciones estamos **comparando sus valores de referencia y no su contenido en memoria**. La única forma de que cuando se comparan dos objetos con el operador `===` se obtenga un valor `true` es que ambos objetos tengan **la misma referencia a la posición de memoria**. Por esta cuestión, al operador `===` también se le denomina **operador identidad**, ya que cuando comparamos dos objetos nos informa si ocupan la misma posición de memoria.

Nos quedaría pendiente una última cuestión: Cómo saber si dos objetos que ocupan posiciones distintas en memoria tienen igual contenido. Esta es una operación que JS **no resuelve de forma trivial** y que no es recomendable hacer salvo que no haya más remedio. Llegados a este punto se tendrían dos opciones:

- Usar `JSON.stringify` para convertir un objeto a una cadena `string` y después implementar la comparación
- Usar una librería externa como Lodash, que implementa métodos como `.isEqual` y que permiten la comparación de contenidos de dos objetos distintos iterando de forma recursiva sobre todas sus propiedades.

## El operador typeof

Aplicado a una variable o datos de tipo primitivo el funcionamiento es sencillo: nos devuelve un `string` con el tipo en cuestión. Sin embargo, cuando se aplica a un tipo no-primitivo siempre devuelve el valor `“object”`. Esto hace que dicho operador, siendo muy útil para distinguir tipos primitivos de los que no lo son, sea completamente inútil para **distinguir entre distintos tipos de objetos** en JS. Para ello podemos usar el operador `instanceof`, que permite distinguir **entre tipos de objetos nativos** (pero que no funciona con tipos primitivos!!)

Un mecanismo interesante para conocer el tipo de un dato, cuando no podemos hacerlo con `instanceof` o con `typeof` es el denominado *Duck-Typing*. Consiste en chequear **el comportamiento del objeto** siguiendo una máxima: *Si anda como un pato y hace cuak... es un pato*. Para ello tendremos que implementar funciones que hagan el trabajo según cada caso.
