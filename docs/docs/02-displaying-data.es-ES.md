---
id: displaying-data-es-ES
title: Mostrando Datos
permalink: displaying-data-es-ES.html
prev: why-react-es-ES.html
next: jsx-in-depth-es-ES.html
---

Lo cosa más básica que puedes hacer con una UI (Interfaz de Usuario) es mostrar algún tipo de dato. React hace sencillo mostrar datos y mantener automáticamente la interfaz `actualizada` cuando los datos cambian.

## Empezando

Veamos un ejemplo muy simple. Crear un archivo `hola-react.html` con el siguiente código:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hola React</title>
    <script src="https://fb.me/react-{{site.react_version}}.js"></script>
    <script src="https://fb.me/react-dom-{{site.react_version}}.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.min.js"></script>
  </head>
  <body>
    <div id="ejemplo"></div>
    <script type="text/babel">

      // ** ¡Su código va aquí! **

    </script>
  </body>
</html>
```

Para el resto de la documentación, sólo tendremos que centrarnos en el código JavaScript y asumir que es insertado en una plantilla como la de arriba. Reemplace el comentario marcado de arriba con el siguiente JSX:

```javascript
var HolaMundo = React.createClass({
  render: function() {
    return (
      <p>
        Hola, <input type="text" placeholder="Tu nombre aquí" />!
        Es {this.props.date.toTimeString()}
      </p>
    );
  }
});

setInterval(function() {
  ReactDOM.render(
    <HolaMundo date={new Date()} />,
    document.getElementById('ejemplo')
  );
}, 500);
```

## Actualizaciones Reactivas

Abrir Hola-react.html` en un navegador web y escriba su nombre en el campo de texto. Tenga en cuenta que React está cambiando solo la cadena de texto con la fecha en la UI - cualquier dato que pongas en la entrada de texto, incluso si no ha escript ningún código para gestionar este comportamiento. React lo resuelve por usted y hace lo correcto.

La forma en la que es capaz de resolver esto es que React no manipula el DOM a menos que lo necesite. ** Lo hace rápido, usa una maqueta interna del DOM para llevar a cabo las diferenciaciones y calcular la mutación del DOM de una forma eficiente. **

Las entradas a este componente se llaman `props` - abreviatura de "propiedades". Ellos son pasados como atributos en la sintaxis JSX. Deben de pensar en ellos como inmutables dentro del componente, es decir, ** Nunca sobrescribir a `this.props` **.

## Los Componentes son Sólo Como Funciones

Lo componentes de React son muy simples. Se puede pensar en ellos como funciones simples que tienen `props` y `state` (explicado más adelante) y muestran HTML. Con esto en mente, los componentes son fáciles de entender.

> Nota:
>
> **Una limitación**: Lo componentes de React solo pueden generar un único nodo raíz. Si desea devolver múltiples nodos  *debe* ser envuelto en una sola raíz.

## Syntax de JSX

Creemos firmemente que los componentes son la manera correcta de separar preocupaciones en lugar de "plantillas" y "lógica de visualización." Creemos que el marcado y el código que genera que están íntimamente vinculados entre sí. Además, la lógica de visualización es a menudo muy compleja y el uso de lenguajes de plantillas para expresar se vuelve muy complicado.

Hemos encontrado que la mejor solución para este problema es generar HTML y arboles de componentes directamente desde el código JavaScript de tal manera que se puede utilizar toda la potencia expresiva de un lenguaje de programación real para construir interfaces de usuario.

Con el fin de hacer esto más fácil, hemos añadido una muy simple, sintaxis **opcional** como HTML para crear estos arboles de nodos en React.

**JSX te permite crear objetos de JavaScript utilizando la sintaxis HTML** Para generar un link en React usando JavaScript puro puedes escribir lo siguiente:

`React.createElement('a', {href: 'https://facebook.github.io/react/'}, '¡Hola!')`

Con JSX esto se convierte en:

`<a href="https://facebook.github.io/react/">¡Hola!</a>`

Hemos descubierto que esto hace que la construcción de aplicaciones en React sea más fácil y diseñadores tiendan a preferir esta sintaxis, pero cada uno tiene su propio flujo de trabajo, por lo que **JSX no está obligado a utilizarse en React.**

JSX es muy pequeño. Para obtener más información al respecto, véase [JSX en profundidad]

JSX es muy pequeño. Para obtener más información al respecto, véase [JSX a fondo](/react/docs/jsx-in-depth-es-ES.html). O ver la transformación en acción en [Babel REPL](https://babeljs.io/repl/).

JSX es similar a HTML, pero no es exactamente lo mismo. Ver [trampas JSX]  para algunas diferencias clave.

JSX es similar a HTML, pero no es exactamente lo mismo. Ver [aspectos críticos de JSX](/react/docs/jsx-gotchas-es-ES.html) para algunas diferencias importantes.

que van desde herramientas de línea de comandos a integraciones de Ruby on Rails. Seleccione la herramienta que funcione mejor para usted.

[Babel expone una serie de maneras de comenzar a usar JSX](http://babeljs.io/docs/setup/), que van desde herramientas de línea de comandos a integraciones de Ruby on Rails. Seleccione la herramienta que mejor funcione para usted.

## React sin JSX

JSX es completamente opcional; usted no tiene que utilizar JSX con React. Puede crear elementos de React en JavaScript puro utilizando `React.createElement`, que toma un nombre de etiqueta o componente, un objeto de propiedades, y el número variable de argumentos secundarios opcionales.

```javascript
var secundario1 = React.createElement('li', null, 'First Text Content');
var secundario2 = React.createElement('li', null, 'Second Text Content');
var root = React.createElement('ul', { className: 'my-list' }, secundario1, secundario2);
ReactDOM.render(root, document.getElementById('ejemplo'));
```

Para mayor comodidad, puede crear funciones cortas a mano para crear elementos de componentes personalizados.

```javascript
var Factory = React.createFactory(ComponentClass);
...
var root = Factory({ custom: 'prop' });
ReactDOM.render(root, document.getElementById('ejemplo'));
```

React ya ha integrado funciones de etiquetas HTML comunes:

```javascript
var root = React.DOM.ul({ className: 'mi-lista' },
             React.DOM.li(null, 'Contenido del Texto')
           );
```
