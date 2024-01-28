## Módulos en JavaScript

En sus primeras versiones, JS no implementó funciones nativas que manejaran espacios de nombres y módulos. Para suplir esta carencia se fueron introduciendo con el tiempo diferentes patrones de diseño. Vamos a reseñar algunos de ellos:

### Funciones IIFE

Se han visto en el apartado anterior. Es una manera interesante de escribir módulos para usar con navegadores muy antiguos. Implementa el **patrón Singleton**, creando una única instancia de los objetos y del código y proporcionando un único punto de acceso global a ella. Podemos concatenar archivos distintos sin preocuparnos de los espacios de nombres. El problema es que la carga de estas funciones es sincrónica, por lo que **tendremos que tener en cuenta el orden** de uso de las mismas.

```javascript
(function () {
  // Código del módulo
})();
```

### CommonJS (CJS)

Es el sistema de módulos nativo de Node.JS. En este patrón, cada archivo representa un módulo y cada una de las variables locales de dicho módulo es privada. Se usa la sintaxis `module.export` o `export`. En tiempo de ejecución Node.JS envolverá todo el módulo en un contenedor de funciones y se dispondrá de ellos gracias a una sentencia `require`. La ventaja de usar CommonJS es que, aunque la carga de los módulos es síncrona, CommonJS organiza las llamadas a los módulos de forma que se satisfagan las dependencias circulares. La desventaja principal, sin embargo, es que este sistema **no es el más adecuado** para aplicaciones del lado del cliente. Veamos un ejemplo:

```javascript
// module-name.js
module.exports = {
  /* ... */
}

// index.js
const module = require("./module-name.js");
const package = require("package");

module.method();
```

### Asynchronous Module Definition (AMD) 

AMD nace a partir de las limitaciones de CJS a la hora de implementarse del lado del cliente. Su sintaxis es más compleja de entender y no alcanzó el nivel de popularidad de CJS. La estructura es del tipo `define(deps, module)`. Veamos un ejemplo:

```javascript
define(['dep1', 'dep2'], function (dep1, dep2) {
  /* ... */

  return {
    /* ... */
  };
});
```

El array `['dep1', 'dep2']` contiene las dependencias que se necesitan para ejecutar el módulo (function()). Si están cargadas, se ejecuta, si no, se carga asíncronamente hasta que estén disponibles. La implementación más interesante de este patrón fue `require.js`, sin embargo, con la llegada de un sistema nativo de módulos a JS con la especificación ES6. Este sistema de módulos y todos los anteriores pasaron a un segundo plano.

### ES Modules (ESM)

Con ECMAScript 2015 (ES6) aparece un sistema de módulos nativo y fácil de usar. Recoger, de manera simple, lo mejor de los patrones anteriores. Veamos un ejemplo que ya nos resultará más familiar

```javascript
// module.js
export const data = "Frodo";
export const method = (data) => console.log(`"Hello, ${data}`);

// index.js
import { data, method } from "./module.js";
```

###  Diferencias entre CJS y ESM

Repasemos por último algunas diferencias entre los sistemas de módulos CJS y ESM

- NodeJS soporta tradicionalmente la sintaxis `require` de **CommonJS**, y aunque cada vez soporta mejor **ESM**, aún no es completo. Tiene una amplia comunidad que usa **CommonJS** a través de **NPM**.
- **CommonJS** sólo permite cargar módulos de forma síncrona, mientras que **ESM** permite carga síncrona y asíncrona.
- Los `require` de **CommonJS** no son compatibles en el navegador de forma directa, mientras que los `import` de **ESM** si lo son si se indica el atributo `<script type="module">` en los scripts que los utilicen.
- **CommonJS** no permite cargar directamente desde una URL o CDN un módulo, mientras que con **ESM** puedes hacerlo sin problemas y funciona directamente desde un navegador.
