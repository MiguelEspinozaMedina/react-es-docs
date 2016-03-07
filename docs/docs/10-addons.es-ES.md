---
id: addons-es-ES
title: Complementos
permalink: addons-es-ES.html
prev: tooling-integration-es-ES.html
next: animation-es-ES.html
---

Los Complementos de React son una colección de módulos de servicios útilies para la construcción de aplicaciones con React. **Esto debe de ser considerado experimental** y tiende a cambiar más a menudo que el núcleo.

- [`TransitionGroup` and `CSSTransitionGroup`](animation-es-ES.html), para hacer frente a las animaciones y transiciones que son por lo general son complejas de implementar, por ejemplo, antes de remover un componente.
- [`LinkedStateMixin`](two-way-binding-helpers-es-ES.html), para simplificar la coordinación entre la introducción de datos a través de formularios por parte del usuario y los estados del componente.
- [`cloneWithProps`](clone-with-props-es-ES.html), para hacer copias de componentes de React y cambiarle sus props.
- [`createFragment`](create-fragment-es-ES.html), para crear un conjunto de hijos acuñados externamente.
- [`update`](update-es-ES.html), una función auxiliar que sirve para tratar datos inmutables en JavaScript de una forma sencilla.
- [`PureRenderMixin`](pure-render-mixin-es-ES.html), un refuerzo de rendimiento para ciertas situaciones.
- [`shallowCompare`](shallow-compare-es-ES.html), una función auxiliar que realiza una comparación para los props y el estado de un componente para decidir si un componente debe actualizarse.

Los complementos de abajo estan solo en la version de desarrollo (desminificado) de React
The add-ons below are in the development (unminified) version of React only:

- [`TestUtils`](test-utils.html), simple utilidad auxiliar para escribir casos de pruebas.
- [`Perf`](perf.html), una herramienta de perfiles de rendimiento para encontrar oportunidades de optimización.

Para obtener los complementos, instalalos individualmente desde npm (ejm: `npm install react-addons-pure-render-mixin`). No damos soporte para el uso de los complementos si no estas usando npm.
