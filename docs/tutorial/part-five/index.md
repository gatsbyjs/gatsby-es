---
title: Plugins fuente
typora-copy-images-to: ./
disableTableOfContents: true
---

> Este tutorial es parte de una serie sobre la capa de datos de Gatsby. Asegúrate de haber terminado la [parte 4](/tutorial/part-four/) antes de continuar aquí.

## ¿Qué contiene este tutorial?

En este tutorial aprenderás cómo consumir datos en tu sitio de Gatsby usando GraphQL y plugins fuente. Sin embargo, antes de aprender acerca de estos plugins, será bueno saber cómo usar algo llamado GraphiQL, una herramienta que te ayuda a estructurar tus consultas de manera correcta.

## Presentando GraphiQL

GraphiQL es el entorno de desarrollo integrado para GraphQL. Es una herramienta poderosa (y asombrosa) que usarás a menudo al crear sitios web de Gatsby.

Puedes usarla cuando tu sitio de desarrollo esté ejecutándose de forma habitual en
`http://localhost:8000/___graphql`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Your browser does not support the video element.</p>
</video>

Investiga un poco el tipo de dato `Site` que viene preconfigurado y mira qué campos están disponibles dentro de él, incluyendo el `siteMetadata` que consultaste antes. ¡Intenta abrir GraphiQL y juega con tus datos! Presiona <kbd> Ctrl + Espacio </kbd> (o usa <kbd> Shift + Espacio </kbd> como un atajo de teclado alternativo) para abrir la ventana de autocompletado y <kbd> Ctrl + Enter </kbd> para ejecutar la consulta GraphQL. Utilizarás GraphiQL mucho más durante el resto del tutorial.

## Usando el explorador de GraphiQL

El explorador de GraphiQL te permite construir consultas de manera interactiva, haciendo clic en los campos y entradas disponibles, evitando el repetitivo proceso de escribir tales consultas a mano.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer"
  lessonTitle="Build a GraphQL Query using Gatsby’s GraphiQL Explorer"
/>

## Plugins fuente

Los datos en los sitios de Gatsby pueden venir de cualquier parte: API, bases de datos, CMS, archivos locales, etc.

Los plugins fuente obtienen datos de su fuente. P.ej. el plugin fuente del sistema de archivos sabe cómo obtener datos del sistema de archivos. El plugin de WordPress sabe cómo obtener datos de la API de WordPress.

Añade [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) y explora cómo funciona.

Primero, instala el plugin en la raíz de tu proyecto:

```shell
npm install --save gatsby-source-filesystem
```

Luego añádelo en tu archivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Comiendo Mucho`,
  },
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    // highlight-end
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

Guarda esto y reinicia el servidor de desarrollo de gatsby. Luego abre GraphiQL nuevamente.

En el planel de exploración verás `allFile` y `file` disponibles en tus selecciones:

![graphiql-filesystem](graphiql-filesystem.png)

Haz clic en el desplegable de `allFile`. Posiciona tu cursor tras `allFile` en la zona de tu consulta y presiona <kbd>Ctrl + Enter</kbd>. Esto autocompletará tu consulta con el `id` de cada archivo. Presiona "Reproducir" para ejecutarla:

![filesystem-query](filesystem-query.png)

En el panel de Explorador, el campo `id` se ha seleccionado automáticamente. Haz selecciones para más campos haciendo clic en sus correspondientes casillas. Presiona "Reproducir" para ejecutar nuevamente la consulta con los nuevos campos:

![filesystem-explorer-options](filesystem-explorer-options.png)

Alternativamente, puedes agregar campos utilizando el atajo de teclado de autocompletar (<kbd> Ctrl + Espacio </kbd>). Esto mostrará campos consultables en los nodos `File`.

![filesystem-autocomplete](filesystem-autocomplete.png)

Prueba a añadir un número de campos a tu consulta presionando <kbd>Ctrl + Enter</kbd>
cada vez para volver a ejecutarla. Verás sus resultados actualizados:

![allfile-query](allfile-query.png)

El resultado es un _array_ de "nodos" `File` (un nodo es una forma elegante de nombrar un objeto en un
"grafo"). Cada objeto nodo `File` contiene los campos que consultaste.

## Construye una página con una consulta de GraphQL

La construcción de nuevas páginas con Gatsby a menudo comienza en GraphiQL. Primero esbozas
la consulta de datos jugando en GraphiQL y luego la copias a un componente de página de React
para empezar a crear la UI.

Probemos esto.

Crea un nuevo archivo `src/pages/my-files.js` con la consulta `allFile` de GraphQL que acabas de
crear:

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data) // highlight-line
  return (
    <Layout>
      <div>Hola mundo</div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

La línea `console.log(data)` es resaltada más arriba. Normalmente es de ayuda, al crear un componente,
mostrar en la consola la información que recibimos de la consulta de GraphQL
de tal forma que puedas explorar en tu consola de navegador mientras construyes la UI.

Si visitas la nueva página en `/my-files/` y abres tu consola del navegador
verás algo como:

![data-in-console](data-in-console.png)

La forma de los datos coincide con la forma de la consulta GraphQL.

Añade algo de código a tu componente para mostrar la información de File.

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>Los Archivos de Mi Sitio</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

Visita ahora `http://localhost:8000/my-files`… 😲

![my-files-page](my-files-page.png)

## ¿Qué viene luego?

Has aprendido cómo los plugins fuente agregan información _dentro_ del sistema de datos de Gatsby. En el siguiente tutorial, aprenderás cómo los plugins transformadores _transforman_ el contenido bruto aportado por los plugins fuente. La combinación de plugins fuente y transformadores puede gestionar toda la fuente y transformación de datos que necesites al construir un sitio de Gatsby. Aprende sobre los plugins transformadores en la [parte seis del tutorial](/tutorial/part-six/).
