---
title: Data in Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

¡Bienvenido a la Parte 4 del tutorial! ¡Hemos llegado a la mitad! Esperamos que comiences a sentirte bastante cómodo. 😀

## Resumen de la primera parte del tutorial

Hasta ahora, has estado aprendiendo cómo usar React.js, lo poderoso que es ser capaz de crear tus _propios_ componentes para actuar como bloques personalizados para construir sitios web.

También has explorado componentes de estilo usando Módulos CSS.

## Qué encontrarás en este tutorial

En las próximas cuatro partes del tutorial (incluyendo esta), bucearás en la capa de datos de Gatsby, que es una catacterística muy poderosa de Gatsby que te permite construir con facilidad sitios desde Markdown, WordPress, CMSs sin cabeceras y otras fuentes de datos de todos los sabores.

**NOTA:** La capa de datos de Gatsby utiliza GraphQL. Para un tutorial en profundidad sobre GraphQL, recomendamos [Cómo GraphQL](https://www.howtographql.com/).

## Datos en Gatsby

Una página web tiene cuatro partes: HTML, CSS, JS, y datos. La primera parte del tutorial nos hemos centrado en los primeros tres. Ahora vamos a aprender a manejar datos en sitios de Gatsby.

**¿Qué son datos?**

Una manera muy informática de responder sería que datos son cosas como `"strings"`,
integers (`42`), objects (`{ pizza: true }`), etc.

Para el propósito de trabajar en Gatsby, por otra parte, una forma de responder más útil es: "todo lo que reside fuera de un componente React"

Hasta ahora, has estado codificando texto y añadiendo imágenes _directamente_ en componentes. Lo que es una manera _excelente_ de construir muchas sitios web, Pero, a menudo quieres almacenar datos en componentes _externos_ y llevar los datos _dentro_ del componente cuando es necesario.

Si has estado creando un sitio web con WordPress (así otros contribuyentes tienen una interfaz bonita para añadir y mantener el contenido) y Gatsby, los _datos_ para el sitio (páginas y entradas) están en WordPress y tu _obtienes_ los datos, si son necesarios hacia tus componentes.
Los datos también pueden residir en tipos de archivo como Markdown, CSV, etc. así como bases de datos y APIs de todo tipo.

**La capa de datos de Gatsby te permite obtener los datos de esos (y cualquier otra fuente) directamente en tus componentes** en la forma y formato que quieras.

## Usando Datos Desestructurados vs GraphQL

### ¿Tengo que usar GraphQL y plugins de fuentes para llevar datos a sitios web Gatsby?

¡Para nada! Puedes usar la API del nodo `createPages` para llevar los datos desestructurados a las páginas Gatsby directamente, en lugar de a través de la capa de datos GraphQL. Esto es una gran elección para sitios web pequeños, mientras que GraphQL y los plugins de fuente pueden ayudar a ahorrar tiempo en sitios más complejos.

¿Mira la guía [Usando Gatsby sin GraphQL](/docs/using-gatsby-without-graphql/) para aprender como mover datos en tu página Gatsby usando la API de node `createPages` y ¡para ver una pagina de ejemplo!

### ¿Cuándo debo usar datos desestructurados frente a GraphQL?

Si estás creando un sitio web pequeño, una de las formas más eficientes de crearla es obtener los datos en forma desestructurada como hemos remarcado en esta guía, usando la API `createPages` y, si el sitio se hace más complejo más adelante, te toca crear sitios más complejos o te gustaría transformar tus datos, sigue estos pasos:
1.Echa un vistazo a la [Librería de plugins](/plugins/) para ver si los plugins de fuente y o los plugins de transformaciones que te gustaría usar ya existen.
2. Si no existen, lee la guía de [Autorización de plugins](/docs/creating-plugins/) ¡y considera crear el tuyo propio!

### Cómo la capa de datos de Gatsby usa GraphQL para traer datos a los componentes

Hay muchas opciones para cargar datos en los componentes React. Uno de los más populares y poderosos es una tecnología llamada [GraphQL](http://graphql.org/).

GraphQL fue creado por Facebook para ayudar a los ingenieros de producto a _traer_ los datos necesarios en los componentes.

GraphQL es un **l**enguaje de **q**uerys (la parte  _QL_ de su nombre).Si estás familiarizado con SQL, funciona de una forma muy similar. Usando una sintaxis especial, describes los datos que quieres en tu componente y entonces te son proporcionados.

Gatsby usa GraphQL para habilitar componentes para declarar los datos que necesitan.

## Crea un nievo sitio web de ejemplo

Crea otro nuevo sitio para esta parte del tutorial. Vas a crear un blog en Markdown llamado "Pandas Eating Lots". Está dedicado a enseñar las mejores fotos y videos de pandas comiendo montones de comida. Por el camino, comenzarás a conocer el soporte de Gatsby de Markdown y GraphQL.

Abre una nueva ventana de terminal e introduce los siguientes comandos para crear una nueva página Gatsby en un directorio llamado `tutorial-part-four`. Tras esto, abre el nuevo directorio:

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```
Luego instala otras dependencias necesarias en la carpeta raíz del proyecto. Usarás el tema typográfico "Kirkham", y probarás una librería DSS-en-JS, ["Emotion"](https://emotion.sh/):

```shell
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```
Configura un sitio similar al que completaste en la [Parte Tres](/tutorial/part-three). Este sitio tendrá con componente de capa y dos componentes de página:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
  <div
    css={css`
      margin: 0 auto;
      max-width: 700px;
      padding: ${rhythm(2)};
      padding-top: ${rhythm(1.5)};
    `}
  >
    <Link to={`/`}>
      <h3
        css={css`
          margin-bottom: ${rhythm(2)};
          display: inline-block;
          font-style: normal;
        `}
      >
        Pandas Eating Lots
      </h3>
    </Link>
    <Link
      to={`/about/`}
      css={css`
        float: right;
      `}
    >
      About
    </Link>
    {children}
  </div>
)
```

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
      <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
      />
    </div>
  </Layout>
)
```

```jsx:title=src/pages/about.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>About Pandas Eating Lots</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)
```

```javascript:title=src/utils/typography.js
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

`gatsby-config.js` (must be in the root of your project, not under src)

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Añade los archivos de arriba y ejecuta `gatsby develop`, como siempre, deberías ver lo siguiente:

![inicio](start.png)

Tienes otro pequeño sitio con una capa y dos páginas.

Ya puedes comenzar a lanzar peticiones 😋

## Tu primera petición GraphQL

Cuando creas páginas web, probablemente querrás reusar los bits comunes de datos -- como el _titulo del sitio_ por ejemplo. Mira la página 
`/about/`. Te darás cuenta que tienes el titulo de la pagina (`Pandas Eating Lots`) en ls dos componentes de capa (la cabecera del sitio) y en el `<h1 />` de la página `about.js` (cabecera).

Pero, ¿y si quieres cambiar el titulo del sitio en el futuro? Tienes que buscar el título en todos tus componentes y editar cada instancia. Esto es incómodo y genera errores, especialmente en sitios complejos y grandes. En lugar de ello, puedes guardar el título en un lugar y referenciar esa localización desde otros archivos; cambia el título en un lugar y Gatsby _cogerá_ tu título actualizado en los archivos que lo referencien.

El lugar para esos bits comunes de datos es el objeto `siteMetadata` en el archivo  `gatsby-config.js`. Añade tu título del sitio al archivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  // highlight-start
  siteMetadata: {
    title: `Title from siteMetadata`,
  },
  // highlight-end
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Reinicia el servidor de desarrollo.

### Usa una petición de página

Ahora el título del sitio está disponible para ser solicitado; Añádelo al archivo `about.js` usando una [petición de página](/docs/page-query):

```jsx:title=src/pages/about.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-next-line
export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1> {/* highlight-line */}
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)

// highlight-start
export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end
```

Funciona!🎉

![Page title pulling from siteMetadata](site-metadata-title.png)

La petición básica que obtiene el `title` en nuestro `about.js` cambia en:

```graphql:title=src/pages/about.js
{
  site {
    siteMetadata {
      title
    }
  }
}
```

> 💡 En la [parte cinco](/tutorial/part-five/#introducing-graphiql), conocerás una herramienta que nos permite explorar interactivamente los datos disponibles a través de GraphQL, y ayudar a crear peticiones como las de arriba.

Las peticiones de página viven fuera de la definición del componente -- por convencion al final del archivo de componente de página -- y están disponibles únicamente para los componentes de página

### Usa una Petición Estática

[StaticQuery](/docs/static-query/) es una nueva API introducida en la versión 2 de Gatsby que permite componentes que no son de página (como nuestro componente `layout.js`), obtener datos via peticiones GraphQL.
Usemos su nueva versión de ganchos — [`useStaticQuery`](/docs/use-static-query/).

Adelante, haz algunos cambios a tu archivo `src/components/layout.js` para usar el gancho `useStaticQuery` y una referencia  `{data.site.siteMetadata.title}`que usa esos datos. Cuando hayas terminado, tu archivo se parecerá a esto:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
// highlight-next-line
import { useStaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"
// highlight-start
export default ({ children }) => {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  return (
    // highlight-end
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          {data.site.siteMetadata.title} {/* highlight-line */}
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
    // highlight-start
  )
}
// highlight-end
```

¡Otro éxito! 🎉

![Page title and layout title both pulling from siteMetadata](site-metadata-two-titles.png)

¿Por qué usar dos peticiones distintas aquí? Esos ejemplos son introducciones rápidas a los tipos de peticiones, cómo son formateadas, y dónde pueden ser usadas. Por ahora, ten en cuenta que sólo páginas pueden hacer peticiones de página. Componentes que no son de página, como Layout, puede usar StaticQuery. La [Parte 7](/tutorial/part-seven/) del tutorial lo explica en profundidad.

Pero restauremos el título original.

Uno de los principios principales de Gatsby es que _los creadores necesitan una conexión inmediata a lo que están creando_ ([dicho por Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/)). En otras palabras, cuando haces algun cambio al código, deberías ver inmediatamente el efecto de ese cambio. Si manipulas la entrada de Gatsby verás el cambio en pantalla.

Así que casi en todos los sitios, los cambios que hagas se verán casi instantáneamente. Modifica el archivo `gatsby-config.js` de nuevo, esta vez cambiando el título `title` de nuevo a "Pandas Eating Lots". El cambio debería aparecer muy rápido en las páginas de tu aplicación.

![Both titles say Pandas Eating Lots](pandas-eating-lots-titles.png)

## ¿Qué viene ahora?

Tras esto, aprenderás cómo obtener datos en tu Gatsby usando GraphQL con plugins de fuente en la [Parte Cinco](/tutorial/part-five/) del tutorial.
