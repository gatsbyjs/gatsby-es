---
title: Standard Styling with Global CSS Files
---

Tradicionalmente, los sitios web han sido dotadas de estilos usando archivos globales CSS.

Las reglas de CSS con ámbito global están declaradas en hojas de estilo externas `.css`, y [la especificidad de CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) y [su Cascada](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) determinan como los estilos se aplican.

## Añadiendo estilos globales con un componente de capa

La mejor manera de añadir estilos globales es con un [componente de capa compartido](/tutorial/part-three/#your-first-layout-component). Este componente de capa se usa para cosas que se comparten a lo largo del sitio web, incluyendo estilos, componentes de cabeceras y otros objetos comunes.

> **NOTA:** Este patrón se implementa por defecto en [el inicio por defecto](https://github.com/gatsbyjs/gatsby-starter-default/blob/02324e5b04ea0a66d91c7fe7408b46d0a7eac868/src/layouts/index.js#L6).

Para crear una capa compartida con estilos globales, comienza creando un nuevo sitio Gatsby con el [inicio Hola Mundo](https://github.com/gatsbyjs/gatsby-starter-hello-world).

```shell
gatsby new global-styles https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Abre tu nuevo sitio web en tu editor de código y crea un nuevo directorio en `/src/components`. Dentro, crea dos nuevos archivos:

```diff
  global-styles/
  └───src/
      └───components/
+     │   │─  layout.js
+     │   └─  layout.css
      │
      └───pages/
          └─  index.js
```

Dentro de `src/components/layout.css`, añade algunos estilos globales:

```css:title=src/components/layout.css
div {
  background: red;
  color: white;
}
```

En `src/components/layout.js`, incluye la hoja de estilos y exporta un componente de capa:

```jsx:title=src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

Finalmente, actualiza `src/pages/index.js` para usar el nuevo componente de capa:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Hello world!</Layout>
```

Ejecuta `npm run develop` y verás los estilos globales aplicados.

![Global styles](./images/global-styles.png)

## Añadiendo estilos globales sin un componente de capa

En algunos casos, usar un componente de capa compartido no es deseable. En esos casos, puedes incluir una hoja de estilos global usando `gatsby-browser.js`.

> **NOTA:** Esta aproximación _no_ funciona con CSS-in-JS. Usa componentes compartidos para compartir estilos en CSS-in-JS.

Primero, abre una nueva ventana de terminal y ejecuta los siguientes comandos para crear un nuevo sitio por defecto Gatsby y arranca el servidor de desarrollo:

```shell
gatsby new global-style-tutorial https://github.com/gatsbyjs/gatsby-starter-default
cd global-style-tutorial
npm run develop
```

Segundo, crea un archivo CSS y define tantos estilos como quieras. Por ejemplo:

```css:title=src/styles/global.css
html {
  background-color: peachpuff;
}

a {
  color: rebeccapurple;
}
```

Tras eso, incluye la hoja de estilos en tu archivo `gatsby-browser.js`.

> **NOTA:** Esta solucion funciona cuando incluimos CSS ya que esos estilos son extraídos al compilar el JavaScript y no para css-in-js.
> Incluir estilos en un componente de capa o un archivo global-styles.js es tu mejor opción para ello.

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"

// or:
// require('./src/styles/global.css')
```

> _Nota: Puedes usar la sintaxis require o import de Node.js. Además, la localización del archivo de ejemplo css en una carpeta `src/styles` es arbitraria._

Deberías ver tus estilos globales actualizados a lo largo de tu sitio web:

![Global styles example site](./images/global-styles-example.png)

### Importando archivos CSS en componentes

Es posible separar tus estilos CSS en archivos separados para que otros miembros del equipo puedan trabajar independientemente usando CSS tradicional. Puedes entonces [importar archivos directamente](/docs/importing-assets-into-files/) en páginas, modelos, o componentes:

```css:title=menu.css
.menu {
  background-color: black;
  color: #fff;
  display: flex;
}
```

```javascript:title=components/menu.js
import "css/menu.css"
```

Esta aproximación puede simplificar la integración de CSS o estilos [Sass](/packages/gatsby-plugin-sass/) en tu sitio Gatsby permitiendo a los miembros del equipo escribir y consumir CSS tradicional basado en clases. Por otra parte, hay [concesiones](#limitations) que deben ser consideradas respecto al rendimiento y la falta de eliminación del código muerto.

### Añadiendo clases a los componentes

Ya que `class` es una palabra reservada en JavaScript, tendrás que usar la propiedad `className` en su lugar, la cual renderizará como el atributo soportado por el navegador `class` en la salida HTML.

```jsx
<button className="primary">Click me</button>
```

```css
.primary {
  background: orangered;
}
```

### Limitaciones

El mayor problema con los archivos CSS globales es el riesgo de conflictos con los nombres y efectos secundarios colaterales como herencias no deseadas.

Metodologías CSS como BEM pueden ayudar a solucionarlo, pero una solución más moderna es escribir CSS con ámbito local usando  [Modulos CSS](/docs/css-modules/) o [CSS-in-JS](/docs/css-in-js/).
