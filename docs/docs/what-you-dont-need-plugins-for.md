---
title: Para Qué No Necesitas Plugins
---

La mayoría de las funciones de terceros que deseas agregar a tu sitio web seguirán los patrones estándar de JavaScript y React.js para importar paquetes y componer UIs. ¡Estos no requieren un plugin Gatsby!

Algunos ejemplos:

- Importación de paquetes de JavaScript que proporcionan funcionalidad general, como `lodash` o` axios`
- Usando componentes o bibliotecas de componentes de React que quieres incluir en tu UI, como `Ant Design`,` Material UI` o el typeahead de tu biblioteca de componentes.
- Integrando bibliotecas de visualización, como `Highcharts` o `d3`.

Como regla general, puedes usar cualquier paquete npm que puedes usar sin Gatsby, con Gatsby. Lo que ofrecen los plugins es una integración preempaquetada en las principales API de Gatsby para ahorrarte tiempo y energía, con una configuración mínima. En el caso de los `Styled Components`, puedes renderizar manualmente el componente `Provider` cerca de la raíz de tu aplicación, o simplemente puede usar `gatsby-plugin-styled-components` que se ocupa de este paso por ti además de cualquier otra dificultad que puedas tener para configurar los componentes diseñados para trabajar con la representación del lado del servidor.
