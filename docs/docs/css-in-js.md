---
title: Mejora tus estilos con CSS-in-JS
overview: true
---

CSS-in-JS se refiere a un enfoque donde los estilos son escritos en JavaScript en lugar de un fichero CSS externo para facilitar la separación de estilos entre componentes, fomentando un rendimiento más rápido, estilos dinámicos y mucho más.

CSS-in-JS une la brecha entre CSS y JavaScript:

1. **Componentes**: darás estilo a tu sitio con componentes, integrándose perfectamente con la filosofía "todo es un componente" de React.
2. **Ámbito**: es un efecto colateral de lo primero. Al igual que los [CSS Modules](/docs/css-modules/), por defecto, el CSS-in-JS se encuentra aislado dentro de los componentes.
3. **Dinámico**: da estilo a tu sitio de forma dinámica mediante el estado de tu componente usando variables de JavaScript.
4. **Extras**: muchas bibliotecas de CSS-in-JS generan nombres de clase únicos que pueden ayudar con el _caching_, el _vendor prefix_ automático, la carga oportuna de CSS crítico, y además de implementar muchas otras características, dependiendo de la librería que elijas.

CSS-in-JS, aunque no es obligatorio en Gatsby, es muy popular entre los desarrolladores de JavaScript por las razones que se enumeraron arriba. Para más contexto, lee el artículo de Max Stoiber (creador de la biblioteca de CSS-in-JS [styled-components](/docs/styled-components/)) [_Why I write CSS in JavaScript_](https://mxstbr.com/thoughts/css-in-js/). Sin embargo, también deberías considerar si el CSS-in-JS es necesario, ya que no depender de él puede fomentar un conjunto de habilidades _frontend_ más inclusivas. También es más difícil migrar estilos desde JSX a CSS y viceversa.

_Ten en cuenta que esta funcionalidad no es parte de React o Gatsby, y requiere usar alguna de las muchas [bibliotecas CSS-in-JS de terceros](https://github.com/MicheleBertoli/css-in-js#css-in-js)._

> Añadiendo una clase estable de CSS a JSX junto con CSS-in-JS puede hacer más fácil para tus usuarios incluir [_User Stylesheets_](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para accesibilidad. Veáse un ejemplo con [Styled Components](/docs/styled-components#enabling-user-stylesheets-with-a-stable-class-name).

Esta sección puede contener guías para dar estilo a tu sitio con algunas de las bibliotecas CSS-in-JS más populares, incluyendo cómo configurar estilos globales usando cada biblioteca.

<GuideList slug={props.slug} />
