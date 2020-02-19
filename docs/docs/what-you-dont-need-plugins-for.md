---
title: Para Qué No Necesitas Plugins
---

La mayoría de las funciones de terceros que deseas agregar a tu sitio web seguirán los patrones estándar de JavaScript y React.js para importar paquetes y componer UIs. ¡Estos no requieren un plugin Gatsby!

Algunos ejemplos:

<<<<<<< HEAD
- Importación de paquetes de JavaScript que proporcionan funcionalidad general, como `lodash` o` axios`
- Usando componentes o bibliotecas de componentes de React que quieres incluir en tu UI, como `Ant Design`,` Material UI` o el typeahead de tu biblioteca de componentes.
- Integrando bibliotecas de visualización, como `Highcharts` o `d3`.

Como regla general, puedes usar cualquier paquete npm que puedes usar sin Gatsby, con Gatsby. Lo que ofrecen los plugins es una integración preempaquetada en las principales API de Gatsby para ahorrarte tiempo y energía, con una configuración mínima. En el caso de los `Styled Components`, puedes renderizar manualmente el componente `Provider` cerca de la raíz de tu aplicación, o simplemente puede usar `gatsby-plugin-styled-components` que se ocupa de este paso por ti además de cualquier otra dificultad que puedas tener para configurar los componentes diseñados para trabajar con la representación del lado del servidor.
=======
- Importing JavaScript packages that provide general functionality, such as `lodash` or `axios`
- Integrating visualization libraries, such as `Highcharts` or `d3`.

As a general rule, any npm package you might use while working on another JavaScript or React application can also be used ,with a Gatsby application. What plugins offer is a prepackaged integration into the core Gatsby APIs to save you time and energy, with minimal configuration.

A good use case would be using `Styled Components`, you could manually render the `Provider` component near the root of your application, or you could use [gatsby-plugin-styled-components](https://www.gatsbyjs.org/packages/gatsby-plugin-styled-components/) which takes care of this step for you in addition to any other difficulties when configuring Styled Components to work with server-side rendering.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc
