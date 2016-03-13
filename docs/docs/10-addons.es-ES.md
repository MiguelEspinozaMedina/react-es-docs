---
id: addons-es-ES
title: Complementos
permalink: addons-es-ES.html
prev: tooling-integration-es-ES.html
next: animation-es-ES.html
---

Los Complementos de React son una colección de módulos de utilidad que sirven para la construcción de aplicaciones con React. **Esto debe de ser considerado experimental** y tiende a cambiar más a menudo que el núcleo.

- [`TransitionGroup` and `CSSTransitionGroup`](animation-es-ES.html), para hacer frente a las animaciones y transiciones que, por lo general, no son fáciles de implementar. Por ejemplo, antes de remover un componente.
- [`LinkedStateMixin`](two-way-binding-helpers-es-ES.html), para simplificar la coordinación entre la introducción de datos a través de formularios por parte del usuario y los estados del componente.
- [`cloneWithProps`](clone-with-props-es-ES.html), para hacer copias superfluas de componentes de React y cambiarle sus props.
- [`createFragment`](create-fragment-es-ES.html), para crear un conjunto de componentes hijos que tengan una clave (key) exterior.
- [`update`](update-es-ES.html), una función auxiliar que sirve para facilitar el uso de datos inmutables en JavaScript.
- [`PureRenderMixin`](pure-render-mixin-es-ES.html), un refuerzo de rendimiento para ciertas situaciones.
- [`shallowCompare`](shallow-compare-es-ES.html), una función auxiliar que realiza una comparación suprelfua de los props y el estado de un componente para decidir si un componente debe actualizarse.

Los siguientes complementos se encuentran sólo en la versión de desarrollo (versión no desminuida) de React:

- [`TestUtils`](test-utils.html), utilidad auxiliar simple para escribir casos de pruebas.
- [`Perf`](perf.html), una herramienta de perfiles de rendimiento para encontrar oportunidades de optimización.

Para obtener los complementos, debes instalarlos individualmente desde npm (ejm: `npm install react-addons-pure-render-mixin`). No recomendamos el uso de los complementos si no estas usando npm.
