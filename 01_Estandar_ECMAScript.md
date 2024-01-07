# Información general: Estándar ECMAScript

JavaScript es un lenguaje dinámico múltiparadigma con tipos y operadores, objetos estándar integrados y métodos. Su sintaxis puede encontrar similitudes en los lenguajes Java o C. **JavaScript admite la programación orientada a objetos con prototipos** de objetos, en lugar de clases. JavaScript **también admite la programación funcional**, ya que las funciones se pueden almacenar en variables y pasarse como cualquier otro objeto.

El estándar Ecma actual define el lenguaje ECMAScript 2024. Es la decimoquinta edición de la especificación del lenguaje ECMAScript.

ECMAScript se basa en varias tecnologías de origen, siendo las más conocidas JavaScript (Netscape) y JScript (Microsoft). Como se ha comentado, el lenguaje fue inventado por **Brendan Eich en Netscape** y apareció por primera vez en el navegador Navigator 2.0 de esa compañía. Ha aparecido en todos los navegadores posteriores de Netscape y en todos los navegadores de Microsoft a partir de Internet Explorer 3.0.

El desarrollo de **la especificación del lenguaje ECMAScript comenzó en noviembre de 1996**. La primera edición de esta Norma Ecma fue adoptada por la Asamblea General de Ecma de junio de 1997.

Fue **después de la publicación de la tercera edición**, cuando ECMAScript logró una adopción masiva en el seno de la WWW, donde se ha convertido en el **lenguaje de programación compatible con prácticamente todos los navegadores web**.

La quinta edición de ECMAScript codificó las interpretaciones de facto de la especificación del lenguaje que se habían vuelto comunes entre las implementaciones de los distintos navegadores y agregó soporte para nuevas características que habían surgido desde la publicación de la tercera edición, como por ejemplo la compatibilidad con el formato de codificación de objetos JSON; o un modo estricto (*Strict Mode*), que proporciona una comprobación de errores y una seguridad de programa mejoradas. La quinta edición fue adoptada por la Asamblea General de la ECMA en **diciembre de 2009**.

Sin embargo, es la sexta edición la que marcará un antes y un después en la especificación ECMAScript. Los objetivos de esta edición incluían proporcionar un mejor soporte para aplicaciones grandes, la creación de bibliotecas y el uso de ECMAScript como destino de compilación para otros lenguajes. Algunas de sus principales mejoras incluían módulos, declaraciones de clase, alcance de bloques léxicos, iteradores y generadores, promesas de programación asíncrona, patrones de desestructuración o llamadas de cola adecuadas. La biblioteca ECMAScript de elementos integrados se amplió para admitir abstracciones de datos adicionales, incluidos mapas, conjuntos y matrices de valores numéricos binarios, así como compatibilidad adicional con caracteres suplementarios Unicode en cadenas y expresiones regulares. 

Además, la sexta edición proporciona la base para mejoras periódicas e incrementales anuales del lenguaje y de la biblioteca. La **sexta edición fue aprobada por la Asamblea General en junio de 2015**.

A partir de este punto, las nuevas versiones de la especificación se han ido lanzando de forma anual hasta 2024

**ECMAScript 2017 (ES8)** introdujo, por ejemplo, un conjunto de funciones asincrónicas que mejoraban la experiencia de desarrollo al proporcionar sintaxis para las funciones que devuelven promesas.

> Puede consultar se el estándar actual de ECMAScript aquí: [Especificación del lenguaje ECMAScript® 2024 (tc39.es)](https://tc39.es/ecma262/#sec-intro)

En ocasiones, algunos navegadores deciden implementar pequeñas funcionalidades de versiones posteriores de ECMAScript antes que otras, para ir testeando y probando características, por lo que no es raro que algunas características de futuras especificaciones puedan estar implementadas en algunos navegadores.

> Puedes consultar una tabla de compatibilidad con ES6 aquí: [ECMAScript 6 compatibility table (compat-table.github.io)](https://compat-table.github.io/compat-table/es6/)

Por lo anterior es muy habitual que cuando se desarrolla con JS exista cierta confusión a la hora de escoger la versión ECMAScript a adoptar como preferencia. Generalmente, existen distintas estrategias ***crossbrowser*** para asegurarse que el código funcionará en todos los navegadores.

## Enfoque conservador

El programador decide crear código **ECMAScript 5**, una versión «segura» que actualmente una gran mayoría de navegadores (*incluído Internet Explorer soporta*). Este enfoque permite asegurarse de que el código funcionará sin problemas en cualquier navegador, pero por otro lado, implica que para muchas tareas deberá escribir mucho código, código extra o no podrá disfrutar de las últimas novedades de JS

## Enfoque delegador

El programador decide delegar la responsabilidad «crossbrowser» a un framework o librería que se encargará de ello. Este enfoque tiene como ventaja que es mucho más cómodo para el programador y ahorra mucho tiempo de desarrollo. Hay que tener en cuenta que se heredan todas las ventajas y desventajas de dicho framework/librería, así como que se adopta como **dependencia** (*sin dicho framework/librería, nuestro código no funcionará*). Además, también se suele perder algo de rendimiento y control sobre el código, aunque en la mayoría de los casos es prácticamente inapreciable.

## Enfoque evergreen

El programador decide no preocuparse de la compatibilidad con navegadores antiguos, sino dar soporte sólo a las últimas versiones de los navegadores (***evergreen browsers***), o incluso sólo a determinados navegadores como **Google Chrome** o **Mozilla Firefox**. Este enfoque suele ser habitual en programadores novatos, empresas que desarrollan aplicaciones **SPA** o proyectos que van dirigidos a un público muy concreto y no están abiertas a un público mayoritario.

## Enfoque transpilador

El programador decide crear código de la última versión de **ECMAScript**. Para asegurarse de que funcione en todos los navegadores, utiliza un **transpilador**, que no es más que un sistema que revisa el código y lo traduce de la versión actual de ECMAScript a **ECMAScript 5**, que es la que leerá el navegador.

La ventaja de este método es que se puede escribir código Javascript moderno y actualizado (*con sus ventajas y novedades*) y cuando los navegadores soporten completamente esa versión de ECMAScript, sólo tendremos que retirar el **transpilador** (*porque no lo necesitaremos*). La desventaja es que hay que preprocesar el código (*cada vez que cambie*) para hacer la traducción. En este sentido, sistemas como [Babel](https://babeljs.io/) son muy utilizados y se encargan de traducir de ECMAScript 6 a ECMAScript 5.

Independientemente del enfoque que se decida utilizar, el programador también puede utilizar **polyfills** o **fallbacks** para asegurarse de que ciertas características funcionarán en navegadores antiguos. También puede utilizar enfoques mixtos.

- Un **polyfill** no es más que una librería o código Javascript que actúa de *parche* para dotar de una característica que el navegador aún no posee hasta que una actualización del navegador la implemente.
- Un **fallback** es algo también muy similar: un fragmento de código que el programador prepara para que en el caso de que algo no entre en funcionamiento, se ofrezca una alternativa.
