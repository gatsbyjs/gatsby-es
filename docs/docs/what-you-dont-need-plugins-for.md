---
title: Para qué no necesita Plugins
---

La mayoría de las funciones de terceros que desea agregar a su sitio web seguirán los patrones estándar de JavaScript y React.js para importar paquetes y componer UIs. ¡Estos no requieren un plugin Gatsby!

Algunos ejemplos:

- Importación de paquetes de JavaScript que proporcionan funcionalidad general, como `lodash` o` axios`
- Usando React componentes o bibliotecas de componentes que desea incluir en su interfaz de usuario, como `Ant Design`,` Material UI` o el tipo de letra de su biblioteca de componentes.
- Integrando bibliotecas de visualización, como `Highcharts` o` d3`.

Como regla general, puede usar cualquier paquete npm que pueda usar sin Gatsby, con Gatsby. Lo que ofrecen los plugins es una integración preempaquetada en las principales API de Gatsby para ahorrarle tiempo y energía, con una configuración mínima. En el caso de los `Styled Components`, puede renderizar manualmente el componente `Provider` cerca de la raíz de su aplicación, o simplemente puede usar `gatsby-plugin-styled-components` que se ocupa de este paso por usted además de cualquier otra dificultad que pueda tener para configurar los componentes diseñados para trabajar con la representación del lado del servidor.
