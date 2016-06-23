---
id: thinking-in-react-es-ES
title: Pensando en React
prev: tutorial-es-ES.html
next: conferences-es-ES.html
redirect_from: 'blog/2013/11/05/thinking-in-react.html'
---

por Pete Hunt

React es, en mi opinión, una manera excelente de construir aplicaciones web grandes y rápidas con JavaScript. Ha escalado muy bien para nosotros en Facebook e Instagram.

Una de la muchas bondades de React es como te hace pensar acerca de las aplicaciones a medida que las vas construyendo. En este artículo, voy a guiarte a través del proceso de construir una tabla de productos con búsqueda usando React.

## Comienza con un prototipo

Imagina que ya tenemos una API JSON y un prototipo elaborado por nuestro diseñador. Nuestro diseñador aparentemente no es muy bueno por que nuestro prototipo se ve así:

![Prototipo](/react/img/blog/thinking-in-react-mock.png)

Nuestra API JSON retorna datos de esta manera:

```
[
  {category: "Sporting Goods", price: "$49.99", stocked: true, name: "Football"},
  {category: "Sporting Goods", price: "$9.99", stocked: true, name: "Baseball"},
  {category: "Sporting Goods", price: "$29.99", stocked: false, name: "Basketball"},
  {category: "Electronics", price: "$99.99", stocked: true, name: "iPod Touch"},
  {category: "Electronics", price: "$399.99", stocked: false, name: "iPhone 5"},
  {category: "Electronics", price: "$199.99", stocked: true, name: "Nexus 7"}
];
```

## Paso 1: Descomponiendo la interfaz en una jerarquía de componentes

Lo primero que debes hacer es dibujar cajas alrededor de cada componente (y sub-componente) en el prototipo y darle a todos un nombre. Si estás trabajando con un diseñador, probablemente el ya haya hecho esto, así que ve y habla con el! Los nombres de las capas de su Photoshop pueden llegar a ser los nombres de tus componentes React!

Pero, ¿cómo saber que debe ser su propio componente? Solo usa las mismas técnicas para decidir si debes crear una nueva función u objeto. Una de esas técnicas es el [principio de responsabilidad individual](https://es.wikipedia.org/wiki/Single_responsibility_principle), es decir, un componente idealmente solo debe hacer una cosa. Si acaba creciendo más de lo debido, debe ser descompuesto en pequeños sub-componentes.

Ya que a menudo estás presentando el modelo de datos JSON al usuario, encontrarás que si tu modelo fue construido correctamente, tu interfaz (y por lo tanto su estructura de componentes) van a calzar muy bien. Eso es porque la interfaz y los modelos de datos tienden a adherirse a la misma *arquitectura de la información*, lo que significa que el trabajo de separar la interfaz de usuario en componentes es a menudo un problema trivial. Solo divídela en componentes que representan exactamente un porción de tu modelo de datos.

![Diagrama de componente](/react/img/blog/thinking-in-react-components.png)

Verás que tenemos cinco componentes en esta aplicacion sencilla. He resaltado en letra cursiva los datos que cada componente representa.  

  1. **`FilterableProductTable` (naranja):** contiene todo el ejemplo
  2. **`SearchBar` (azul):** recibe toda la *entrada del usuario*
  3. **`ProductTable` (verde):** muestra y filtra la  *colección de datos* basado en la *entrada del usuario*
  4. **`ProductCategoryRow` (turquesa):** muestra una cabecera por cada *categoría*
  5. **`ProductRow` (rojo):** muestra una fila por cada *producto*

Si observas a `ProductTable`, verás que la cabecera de la tabla (la que contiene las etiquetas "Name" y "Price") no se encuentra en su propio componente. Esto es una cuestión de preferencia, y hay un argumento para hacerlo en una manera u otra. Para este ejemplo, los deje como parte de `ProductTable` porque es parte de la representación de la *colección de datos* la cual es responsabilidad de `ProductTable`. Sin embargo, si esta cabecera crece hasta un punto de ser demasiado compleja (ej. si tuvieramos que añadir la capacidad de poder ordenar), tendría sentido hacer un componente `ProductTableHeader` propio.

Ahora que hemos identificado los componentes en nuestro prototipo, vamos a organizarlos en una jerarquía. Esto es fácil. Los componentes que aparecen dentro de otro componente en el prototipo deben aparecer como un hijo en la jerarquía:

  * `FilterableProductTable`
    * `SearchBar`
    * `ProductTable`
      * `ProductCategoryRow`
      * `ProductRow`

## Paso 2: Construir una versión estática en React

<iframe width="100%" height="600" src="https://jsfiddle.net/reactjs/yun1vgqb/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Ahora que tienes tu jerarquía de componentes, es el momento de implementar la aplicación. La forma más fácil es construir una versión que tome el modelo de datos y rendericé una interfaz sin interactividad. Lo mejor es separar estos procesos, ya que la construcción de una versión estática requiere de mucho que escribir y nada que pensar, por el contrario, añadir interactividad requiere de mucho que pensar y no mucho que escribir. Veremos por que.

Para construir una versión estática de tu aplicación que rendericé tu modelo de datos, necesitaras construir componentes que re-usen otros componentes y pasar datos usando *props*. Los *props* son una manera de pasar datos desde un padre a un hijo. Si estas familiarizado con el concepto de *state*, **de ninguna manera uses state** para construir esta versión estática. State es reservado solo para la interactividad, es decir, datos que cambian en el tiempo. Ya que esta es una versión estática de la aplicación, no lo necesitas.

Puedes construir tu aplicación desde arriba-abajo o abajo-arriba. Es decir, puedes comenzar con la construcción de los componentes desde el componente más alto en la jerarquía (ej. empezando con `FilterableProductTable`) o con el componente más bajo en ella (`ProductRow`). En casos simples, usualmente es más fácil ir de arriba-abajo, y en proyectos grandes, es más fácil ir de abajo-arriba e ir escribiendo pruebas (tests) mientras se desarrolla.

Al final de este paso, tendrás una librería de componentes re-usables que renderizaran tu modelo de datos. Los componentes solo tendrán metodos `render()` ya que esta es una versión estática de tu aplicación. El componente en la parte superior de la jerarquía (`FilterableProductTable`) tomará tu modelo de datos como prop. Si realizas un cambio en tu modelo de datos y llamas a `ReactDOM.render()` de-nuevo, la interfaz será actualizada. Es fácil de ver como la interfaz se actualiza y dónde hacer cambios ya que no hay nada complicado pasando. El **flujo de datos de una sola dirección (one-way data flow)** de React (también llamado *enlace de una dirección/one-way binding*) mantiene todo modular y rápido.

Basta con ir a la [documentación de React](/react/docs/) si necesitas ayuda ejecutando este paso.

### Una pequeña pausa: props vs state

Hay dos formas de "modelar" datos en React: props and state. Es importante entender la diferencia entre los dos; puedes pasar a la [documentación oficial de React](/react/docs/interactivity-and-dynamic-uis.es-ES.html) si no estás seguro de cual es su diferencia.

## Paso 3: Identificar la representación mínima (pero completa) del estado de la interfaz

Para hacer tu interfaz interactiva, necesitarás poder desencadenar cambios en el modelo de datos subyacente. React hace sencillo esto con el uso de **state**.

Para construir tu aplicación correctamente, primero necesitarás pensar en la representación mínima de estado mutable que tu aplicación necesita. La clave aquí es DRY: *Don't Repeat Yourself (No te repitas)*. Averigua la representación mínima absoluta del estado que tu aplicación necesita y calcula todo los demás que necesites a demanda. Por ejemplo, si estás construyendo una lista TODO (lista de cosas por hacer), solo conserva un array de todos los elementos TODO; no mantengas una variable de state por separado para la cuenta. En su lugar, cuando quieras renderizar la cuenta de los elementos TODO, simplemente toma el tamaño del array de los elementos TODO.

Piensa en todas las piezas de datos que tenemos en nuestra aplicación de ejemplo. Tenemos:

  * La lista original de productos
  * El texto de búsqueda que el usuario ha ingresado
  * El valor del checkbox
  * La lista de productos filtrada

Vamos a ir por cada una de ellas y averiguar cual es state. Simplemente realiza tres preguntas sobre cada pieza de datos:

  1. Es pasada desde un padre a través de props? Si es así, es probable que no sea state.
  2. ¿Se mantiene sin cambios a través del tiempo? Si es así, es probable que no sea state.
  3. ¿Se puede calcular en base a cualquier otro state o props? Si es así, no es state.

La lista original de productos es pasada como props, así que no es state. El texto de búsqueda y el checkbox parecen ser state ya que su valor cambia en el tiempo y no pueden ser calculados desde nada. Y finalmente, la lista de productos filtrada no es state ya que puede ser calculada mediante la combinación de la lista original con el texto de búsqueda y el valor del checkbox.

Así que finalmente, nuestro state es:

  * El texto de búsqueda que el usuario ha ingresado
  * El valor del checkbox

## Paso 4: Identificar donde debe vivir tu state

<iframe width="100%" height="600" src="https://jsfiddle.net/reactjs/zafjbw1e/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

OK, hemos identificado cual es la representación mínima del state de la aplicación. A continuación, necesitamos identificar a que componente afecta, o que componente es *dueño*, de este state.

Recuerda: React se trata de hacer fluir los datos en una sola dirección en la jerarquía de componentes. Puede que no sea inmediatamente claro qué componente debe ser dueño del state. **Esto es a menudo la parte más difícil de entender para los que recién empiezan,** así que sigue estos pasos para averiguarlo:

Por cada pieza de state en tu aplicación:

  * Identifica cada componente que rendericé algo basado en ese state.
  * Encuentra un componente propietario en común (un solo componente por encima de todos los componentes que necesiten el state en la jerarquía).
  * Bien el dueño en común u otro componente más arriba en la jerarquía debe ser dueño del state.
  * Si no puedes encontrar un componente donde tenga sentido mantener el state, crea un nuevo componente solo con el propósito de mantener el state y agrégalo en algún lugar en la jerarquía por encima del componente propietario en común.

Vamos a poner en practica esta estrategia en nuestra aplicación:

  * `ProductTable` necesita filtrar la lista de productos basándose en el state y `SearchBar` necesita mostrar el valor del texto de búsqueda y el estado de selección del checkbox.
  * El componente propietario en común es `FilterableProductTable`.
  * Conceptualmente tiene sentido que el texto del filtro y el valor del checkbox vivan en `FilterableProductTable`

Genial, hemos decidido que nuestro state vive en `FilterableProductTable`. Primero, agrega un método `getInitialState()` a `FilterableProductTable` que retorne `{filterText: '', inStockOnly: false}` para reflejar el state inicial de la aplicación. Luego, envia `filterText` y `inStockOnly` a `ProductTable` y `SearchBar` como un prop. Finalmente, usa estos props para filtrar las filas en `ProductTable` y asignar los valores de los campos del formulario en `SearchBar`.

Puedes empezar a ver como se comportará la aplicación: asigna `filterText` con el valor de `"ball"` y refresca tu aplicación. Verás que los datos en la tabla son actualizados correctamente.

## Step 5: Agregando flujo de datos inverso

<iframe width="100%" height="600" src="https://jsfiddle.net/reactjs/n47gckhr/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Hasta ahora, hemos construido una aplicación que renderiza correctamente en función de los props y state fluyendo a través de la jerarquía. Ahora es tiempo de soportar el flujo de datos de la otra manera: los componentes del formulario que se encuentran abajo en la jerarquía necesitan actualizar el state en `FilterableProductTable`.

React hace que este flujo de datos sea explícito para hacer fácil de entender cómo funciona el programa, pero requiere un poco más de escritura que el tradicional enlace de dos direcciones (two-way data binding).

Si intentas escribir o seleccionar el checkbox en la versión actual del ejemplo, verás que React ignora lo que escribes. Esto es intencional, ya que hemos asignado el prop `value` del `input` para que siempre sea igual al `state` pasado desde `FilterableProductTable`.

Vamos a pensar en lo que queremos que suceda. Queremos asegurarnos de que cada vez que el usuario cambie el formulario, se actualice el state para reflejar la acción del usuario. Ya que los componentes sólo deben actualizar su propio state, `FilterableProductTable` pasará un callback a `SearchBar` el cual se ejecutara cuando el state deba ser actualizado. Podemos utilizar el evento `onChange` en los inputs para ser notificados sobre ello. Y el callback pasado por `FilterableProductTable` llamará a `setState()`, y la aplicación será actualizada.

Aunque esto suena complejo, es realmente sólo unas pocas líneas de código. Y esto hace que sea realmente explícita la forma en que tus datos fluyen a través de la aplicación.

## Y eso es todo

Con suerte, esto te da una idea de cómo pensar acerca de construir componentes y aplicaciónes con React. Si bien puede ser un poco más de escritura a lo que estas acostumbrado, recuerda que el código se lee mucho más de lo que se escribe, y es extremadamente fácil leer este código modular y explícito. En cuanto empieces a construir grandes librerías de componentes, apreciaras esta modularidad y el ser explícito, y con la reutilización de código, tus líneas de código comenzaran a reducirse. :)
