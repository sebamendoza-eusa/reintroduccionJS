# Estructuras de control

JavaScript tiene un conjunto de estructuras de control similar a otros lenguajes de la familia C. Las declaraciones condicionales son compatibles con `if` y `else` y se pueden encadenar

```javascript
var name = "kittens";
if (name == "puppies") {
  name += " woof";
} else if (name == "kittens") {
  name += " meow";
} else {
  name += "!";
}
name == "kittens meow";
```

JavaScript tiene bucles `while` y bucles `do-while`. El primero es bueno para bucles básicos; el segundo bucle para donde deseas asegurarte de que el cuerpo del bucle se ejecute por lo menos una vez:

```javascript
while (true) {
  // ¡un bucle infinito!
}

var input;
do {
  input = get_input();
} while (inputIsNotValid(input));
```

El [bucle `for`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/for) de JavaScript es igual que el de C y Java: te permite proporcione la información de control para tu bucle en una sola línea.

```javascript
for (var i = 0; i < 5; i++) {
  // Se ejecutará 5 veces
}
```

JavaScript también contiene otros dos bucles `for` destacados: [`for...of`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/for...of)

```javascript
for (let value of array) {
  // haz algo con valor
}
```

y [`for...in`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/for...in):

```javascript
for (let property in object) {
  // hacer algo con la propiedad del objeto
}
```

Los operadores `&&` y `||` utilizan **evaluación de cortocircuito**, lo cual significa que la evaluación del segundo operando depende del valor del primero. Esto es útil para verificar objetos nulos antes de acceder a sus atributos:

```javascript
let a = 5;
let b = 10;
let c = 0;

let result1 = a || b; // En este caso, a es verdadero, por lo que result1 será 5
let result2 = a && b; // En este caso, a es verdadero, por lo que result2 será 10
let result3 = c || b; // En este caso, c es falso, pero b es verdadero, por lo que result3 será 10
let result4 = c && b; // En este caso, c es falso, por lo que result4 será 0
```

JavaScript tiene un **operador ternario** para expresiones condicionales. El resultado del operador ternario siempre es un valor

```javascript
let allowed = age > 18 ? "yes" : "no";
```

La instrucción `switch` se puede usar para múltiples ramas según un número o cadena:

```javascript
switch (action) {
  case "draw":
    drawIt();
    break;
  case "eat":
    eatIt();
    break;
  default:
    doNothing();
}
```

Si **no se agrega una instrucción `break`,** la ejecución "caerá" al siguiente nivel. Esto **no es recomendable**. De hecho, es muy buena práctica etiquetar específicamente la caída deliberada con un comentario si es realmente lo que se pretende porque ayuda a la depuración

```javascript
switch (a) {
  case 1: // caída deliberada
  case 2:
    eatIt();
    break;
  default:
    doNothing();
}
```

La cláusula `default` es opcional. Se pueden tener expresiones tanto en la parte del switch como en los casos si se desea; las comparaciones tienen lugar entre los dos utilizando el operador `===`:

```javascript
switch (1 + 3) {
  case 2 + 2:
    yay();
    break;
  default:
    neverhappens();
}
```



