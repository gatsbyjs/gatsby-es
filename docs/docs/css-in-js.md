---
title: Mejora tus estilos con CSS-in-JS
overview: true
---

CSS-in-JS se refiere a un enfoque donde los estilos son escritos en JavaScript en lugar de en un fichero externo de CSS manteniendo fácilmente tus estilos en el ámbito de tus componentes, eliminando código muerto, garantizando un rendimiento más rápido y estilos dinámicos, y mucho más.

CSS-in-JS une la brecha entre CSS y JavaScript:

1. **Componentes**: darás estilo a tu sitio con componentes, integrándose perfectamente con la filosofía de "todo es un componente" de React.
2. **Ámbito**: esto es un efecto colateral de lo primero. Al igual que los [CSS Modules](/docs/css-modules/), el CSS-in-JS se encuentra en el ámbito de los componentes por defecto.
3. **Dinámico**: da estilo a tu sitio dinámicamente basado en el estado de tu componente integrando variables de JavaScript.
4. **Extra**: muchas bibliotecas de CSS-in-JS generan nombres de clase únicos que pueden ayudar con el _caching_, el _vendor prefix_ automático, la carga oportuna de CSS crítico, y además implementan muchas otras características, dependiendo de la librería que elijas.

CSS-in-JS, aunque no es obligatorio en Gatsby, es muy popular entre los desarrolladores de JavaScript por las razones que se listaron arriba. Para más contexto, lee el artículo de Max Stoiber (creador de la biblioteca de CSS-in-JS [styled-components](/docs/styled-components/)) [_Why I write CSS in JavaScript_](https://mxstbr.com/thoughts/css-in-js/). Sin embargo, también deberías considerar si el CSS-in-JS es necesario, ya que no depender de él puede fomentar en un conjuntos de habilidades _frontend_ más inclusivas. También es más difícil migrar estilos desde JSX a CSS y viceversa.

_Tenga en cuenta que esta funcionalidad no es parte de React o Gatsby, y requiere usar alguna de las muchas [bibliotecas de terceros de CSS-in-JS](https://github.com/MicheleBertoli/css-in-js#css-in-js)._

> Añadiendo una clase estable de CSS a JSX junto con CSS-in-JS puede hacer más fácil para tus usuario incluir [_User Stylesheets_](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para accesibilidad. Ver un ejemplo con [Styled Components](/docs/styled-components#enabling-user-stylesheets-with-a-stable-class-name).

Esta sección puede contener guías para dar estilo a tu sitio con algunas de las bibliotecas CSS-in-JS más populares, incluyendo como configurar estilos globales usando cada biblioteca.

<GuideList slug={props.slug} />
