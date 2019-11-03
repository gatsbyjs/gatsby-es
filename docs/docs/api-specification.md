---
title: Especificación de la API
---

Las APIs de Gatsby están diseñadas conceptualmente basándose hasta cierto punto en React.js
para mejorar la coherencia entre los dos sistemas.

Las dos prioridades principales de la API son a) facilitar un ecosistema de plugins robusto
y amplio, y b) encima de eso un ecosistema robusto y amplio de temas (por cierto, los temas
están en espera hasta que salga la v1).

## Prerrequisitos

Si necesitas familiarizarte con el ciclo de vida de Gatsby, lee el resumen [Ciclo de Vida de las APIs de Gatsby](/docs/gatsby-lifecycle-apis/).

## Plugins

Los plugins pueden extender Gatsby de muchas maneras:

- Proporcionando datos (p.e. desde el sistema de archivos, una API o una base de datos)
- Transformando datos de un tipo a otro (p.e. un archivo en markdown a HTML)
- Creando páginas (p.e. todos los archivos en markdown de un directorio son transformados
  en páginas con URLs derivadas de su nombre de archivo)
- Modificando la configuración de webpack (p.e. para opciones de estilo o para añadir soporte
  a lenguajes que compilan-a-js)
- Añadiendo cosas a HTML renderizado (p.e. meta etiquetas, o snippets JS de analíticas como
  Google Analytics)
- Escribiendo cosas para crear un directorio basado en datos del sitio (p.e. un _service worker_,
  sitemap, o _feed_ RSS)

Un plugin puede usar múltiples APIs para alcanzar su objetivo. P.e. el plugin para
la biblioteca de CSS-en-JS [Glamor](/packages/gatsby-plugin-glamor/):

1.  modifica la configuración de webpack para añadir su plugin
2.  añade un plugin de Babel para reemplazar el createElement por defecto de React
3.  modifica el renderizado en el servidor para quitar el CSS crítico en cada
    página renderizada y poner el CSS inline en el `<head>` de esa página HTML.

Los plugins también pueden depender de otros plugins. [El plugin
Sharp](/packages/gatsby-plugin-sharp/) expone una serie de APIs a alto-nivel para
transformar imágenes de las que dependen muchos otros plugins de imágenes de Gatsby.
[gatsby-transformer-remark](/packages/gatsby-transformer-remark/) hace
transformaciones básicas markdown->html pero también expone una API que permite
a otros plugins intervenir en el proceso de conversión, p.e.
[gatsby-remark-prismjs](/packages/gatsby-remark-prismjs/) que añade
resaltado a bloques de código.

Los plugins de transformación están separados de los plugins de origen. Los plugins
de transformación comprueban el tipo de los nuevos nodos creados por los plugins
de origen para decidir si pueden transformarlo o no. Lo que significa que un plugin
de transformación de markdown puede transformar markdown de cualquier fuente sin ninguna
otra configuración, p.e. desde un archivo, un comentario de código o un servicio externo
como Trello que soporta markdown en alguno de sus campos de datos.

Lee
[la lista completa de plugins (solo oficiales por ahora — añadiendo soporte para plugins de comunidad más adelante)](/docs/plugins/).

# API

## Conceptos

- _Página_ — una página del sitio con un nombre de ruta, un componente plantilla y una
  consulta GraphQL opcional.
- _Componente de Página_ — un componente React.js que renderiza una página y puede opcionalmente
  especificar una consulta GraphQL.
- _Extensiones de componente_ - extensiones que pueden resolverse como componentes. `.js`
  y `.jsx` son compatibles por defecto, pero los plugins pueden añadir soporte para
  otros lenguajes que compilan-a-js.
- _Dependencia_ - Gatsby rastrea automáticamente las dependencias entre diferentes objetos.
  P.e. una página puede depender de ciertos nodos. Esto permite la recarga en caliente,
  caching, rebuilds incrementales, etc.
- _Nodo_ — un objeto de datos.
- _Campo de Nodo_ - un campo añadido por un plugin a un nodo que no controla.
- _Enlace de Nodo_ - una conexión entre nodos que se convierte en relaciones de
  GraphQL. Puede crearse de diferentes maneras así como inferirse automáticamente.
  Los enlaces padre/hijo de los nodos y sus nodos derivados transformados son
  enlaces de primera clase.

_Más definiciones y términos se pueden encontrar en el [Glosario](/docs/glossary/)_

## Operadores

- _Create_ — crea algo nuevo
- _Get_ — obtiene algo existente
- _Delete_ — borra algo existente
- _Replace_ — reemplaza algo existente
- _Set_ — une a algo existente

## APIs de Extensión

Gatsby tiene muchos procesos. El más destacado es el proceso de "arranque". Tiene
múltiples subprocesos. Una parte difícil de su diseño es que corren durante el
arranque inicial pero también se mantienen activos durante el desarrollo para
continuar respondiendo a los cambios. Esto es lo que impulsa la recarga en caliente,
que todos los datos de Gatsby están "vivos" y reaccionan a los cambios en el entorno.

El proceso de arranque es el siguiente:

carga configuración del sitio -> carga plugins -> nodos fuente -> nodos de transformación ->
crea esquema graphql -> crea páginas -> compila consultas de componente -> ejecuta consultas ->
fin

Una vez que el arranque inicial ha terminado, un `webpack-dev-server` y un servidor express son iniciados para servir archivos para el flujo de desarrollo con actualizaciones en vivo. En un build de producción, Gatsby se salta el servidor de desarrollo y en su lugar crea el CSS, luego el JavaScript, y después el HTML estático con webpack.

Durante este proceso, hay varios puntos de extensión donde los plugins pueden
intervenir. Todos los procesos principales tiene un `onPre` y `onPost`. P.e. `onPreBootstrap`
y `onPostBootstrap`, `onPreBuild` o `onPostBuild`. Durante el arranque,
los plugins pueden responder en varias fases a APIs como `onCreatePages`,
`onCreateBabelConfig` y `onSourceNodes`.

En cada punto de extensión, Gatsby identifica los plugins que implementan la API y
los llama en serie siguiendo el orden en el `gatsby-config.js` del sitio.

Además de extender las APIs en un nodo, los plugins también pueden implementar APIs de
extensión en el proceso de renderización del servidor y en el navegador. P.e.
`onClientEntry` u `onRouteUpdate`.

Las tres principales inspiraciones para esta API y especificaciones son la API de React.js, especialmente
[el email de @leebyron's sobre la API de React](https://gist.github.com/vjeux/f2b015d230cc1ab18ed1df30550495ed),
la charla ["Cómo Diseñar una Buena API y Por Qué Importas" de Joshua Bloch](https://www.youtube.com/watch?v=heh4OeB9A-c&app=desktop), que diseñó muchas partes de Java, y el plugin de diseño
de [Hapi.js](https://hapijs.com/api).
