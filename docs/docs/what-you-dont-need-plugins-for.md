---
title: Para Qué No Necesitas Plugins
---

La mayoría de las funciones de terceros que deseas agregar a tu sitio web seguirán los patrones estándar de JavaScript y React.js para importar paquetes y componer UIs. ¡Estos no requieren un plugin Gatsby!

Algunos ejemplos:

- Importación de paquetes de JavaScript que proporcionan funcionalidad general, como `lodash` o` axios`
- Integrando bibliotecas de visualización, como `Highcharts` o `d3`.

Como regla general, cualquier paquete de npm que puedas usar mientras trabajas con otro proyecto Javascript o aplicación de React tambien puede ser utilizado con una aplicación de Gatsby. Lo que ofrecen los plugins es una integración pre-empaquetada al núcleo de las APIs de Gatsby para ahorrarte tiempo y energía, con una configuración mínima.

Un buen caso de uso sería utilizar `Styled Components`, podrías renderizar manualmente el componente `Provider` cerca de la raíz de tu aplicación, o puedes usar [gatsby-plugin-styled-components](https://www.gatsbyjs.org/packages/gatsby-plugin-styled-components/) que se encarga de este paso por ti adicionalmente de cualquier dificultad para configurar `Styled Components` para trabajar con renderizado del lado del servidor (SSR).
