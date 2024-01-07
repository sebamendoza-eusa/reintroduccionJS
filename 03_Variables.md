# Variables

En JavaScript, una variable es un **contenedor para almacenar datos**. Los datos pueden ser de diversos tipos tal y como se ha visto en el apartado anterior. Para declarar una variable en JavaScript, se utilizan las palabras clave `var`, `let` o `const`. 

## Asignación por valor vs. asignación por referencia: mutabilidad

¿Qué ocurre cuando una variable cambia su valor? ¿y cuando a una variable se le asigna el valor de otra, que pasa con la segunda cuando cambia la primera? ¿Si pasamos una variable como parámetro a una función y esta cambia su valor, se modifica la variable original?

Para responder a las preguntas anteriores es necesario entender la diferencia **entre valor de una variable y referencia de una variable**.

Cuando declaramos variables, el motor de JS puede albergarlas en dos lugares de la memoria: la pila (*stack*) o el heap (*montón*). Los datos que se guardan en las variables pueden ser **estáticos** o **dinámicos**. Los datos estáticos tienen un tamaño que no cambia y por ello el motor JS les asigna una cantidad fija de memoria, **almacenándolos en la pila**. Los tipos primitivos son de naturaleza estática y por ello se guardan en la pila.

Sin embargo cuando a una variable le asignamos un tipo `Object` ,  `Array` o un objeto función, el motor JS asignará espacio en memoria según vaya siendo necesario, de forma **dinámica**. En estos casos los datos se almacenarán en el *heap*, mientras que **un valor de referencia a la variable** se almacenará en la pila. 

Vamos ahora un poco más allá: Cuando se asigna el valor de una variable que contiene un dato primitivo a otra, el motor **copia el valor** y lo asigna a la nueva variable en la pila. En la pila tendremos así **dos variables separadas**. El cambio del valor de una variable **no afectará a la otra**. Pero cuando hacemos esta misma operación con una variable que contiene un dato **que no es primitivo**, lo que se copiará es **el valor de referencia, pero no el contenido**. Es decir, **en la pila** tendremos dos variables con referencias a los mismos datos. Recordemos que estos datos están en el *heap*. 

Asociado a esta cuestión encontramos el término ***mutabilidad*** en JavaScript. Con ello nos referimos a cómo puede afectar a una variable su posición en la memoria debido a la forma en que se manejan las referencias a los objetos. **Cuando un objeto mutable es modificado, su posición en memoria no cambia**, ya que lo que se modifica son sus propiedades o su contenido, no el objeto en sí. Sin embargo, si se crea un nuevo objeto como resultado de la modificación, este nuevo objeto ocupará una nueva posición en la memoria.

**Los tipos primitivos de JS son inmutables**, lo que significa que una vez que a una variable se le asigna un valor, su posición en memoria no podrá albergar otro valor distinto. Cuando se reasigne el valor de dicha variable, dicho valor se guardará en otra posición de memoria diferente.
