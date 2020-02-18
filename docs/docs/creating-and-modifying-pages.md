---
title: "Creando y Modificando Páginas"
---

Gatsby facilita la creación de tus páginas programáticamente.

Las páginas se pueden crear de tres maneras:

- En el archivo gatsby-node.js de tu sitio implementando la API 
[`createPages`](/docs/node-apis/#createPages)
- El núcleo de Gatsby convierte automáticamente los componentes React en `src/pages` a páginas
- Hay plugins que también pueden implementar `createPages` y crear páginas por ti

También puedes implementar la API [`onCreatePage`](/docs/node-apis/#onCreatePage)
para modificar páginas creadas en el core o plugins o para crear [rutas solo para clientes](/docs/building-apps-with-gatsby/).

## Ayuda para depuración

Para ver qué páginas están siendo creadas por tu código o plugins, puedes consultar
información de la página mientras desarrollas en Graph*i*QL. Pega la siguiente consulta 
en el IDE de Graph*i*QL para tu sitio. El IDE de Graph*i*QL está disponible cuando 
ejecutas el servidor de desarrollo de tu sitio en `HOST:PORT/___graphql` 
ej. `localhost:8000/___graphql`.

```graphql
{
  allSitePage {
    edges {
      node {
        path
        component
        pluginCreator {
          name
          pluginFilepath
        }
      }
    }
  }
}
```

La propiedad `context` acepta un objeto, y podemos pasar cualquier dato al que queramos que la página pueda acceder.

También puedes consultar cualquier dato de `contexto` que tu o los plugins agreguen a las páginas.

> **NOTA:** Hay algunos nombres reservados que _no pueden_ ser utilizados en `contexto`. Son: `path`, `matchPath`, `component`, `componentChunkName`, `pluginCreator___NODE`, y `pluginCreatorId`.

## Crear páginas en gatsby-node.js

A menudo necesitarás crear páginas programaticamente. Por ejemplo, tienes
archivos de markdown donde cada uno debe ser una página.

Este ejemplo asume que cada página de markdown tiene una `ruta` establecida en el frontmatter
del archivo de markdown.

```javascript:title=gatsby-node.js
// Implementa la API de Gatsby "createPages". Esto se llama una vez que la capa de
// datos se inicia para permitir que los plugins creen páginas a partir de datos.
exports.createPages = async ({ graphql, actions, reporter }) => {
  const { createPage } = actions

  // Consulta de nodos de markdown para usar en la creación de páginas.
  const result = await graphql(
    `
      {
        allMarkdownRemark(limit: 1000) {
          edges {
            node {
              frontmatter {
                path
              }
            }
          }
        }
      }
    `
  )

  // Manejar errores
  if (result.errors) {
      reporter.panicOnBuild(`Error while running GraphQL query.`)
      return
  }

  // Crear páginas para cada archivo markdown.
  const blogPostTemplate = path.resolve(`src/templates/blog-post.js`)
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    const path = node.frontmatter.path
    createPage({
      path,
      component: blogPostTemplate,
      // En la consulta graphql de tu plantilla de tu blog, puedes usar path
      // como una variable GraphQL para consultar datos del archivo markdown.
      context: {
        path,
        },
    })
  })
}
```

## Modificar páginas creadas por núcleo o plugins

El núcleo de Gatsby y los plugins pueden crear páginas automáticamente por ti. A veces el
el valor predeterminado no es exactamente lo que deseas y necesitas modificar los objetos 
de páginas creadas.

### Eliminar barras finales

Una razón común para necesitar modificar las páginas creadas automáticamente es eliminar
las barras finales.

Para hacer esto, en el `gatsby-node.js` de tu sitio agregua código similar al siguiente:

_Nota: También hay un plugin que elimina automáticamente todas las barras finales de las páginas:
[gatsby-plugin-remove-trailing-slashes](/packages/gatsby-plugin-remove-trailing-slashes/)_.

_Nota: Si necesitas realizar una acción asincrónica dentro de `onCreatePage`, puedes devolver una promesa o utilizar una función` async`._

```javascript:title=gatsby-node.js
// Reemplazar '/' daría como resultado una cadena vacía que no es válida
const replacePath = path => (path === `/` ? path : path.replace(/\/$/, ``))
// Implementa la API de Gatsby "onCreatePage".
// Esto se llama después de crear cada página.
exports.onCreatePage = ({ page, actions }) => {
  const { createPage, deletePage } = actions

  const oldPage = Object.assign({}, page)
  // Eliminar la barra final a menos que la página esté en /
  page.path = replacePath(page.path)
  if (page.path !== oldPage.path) {
    // Reemplazar nueva página con página anterior
    deletePage(oldPage)
    createPage(page)
  }
}
```

### Pasar contexto a páginas

Las páginas creadas automáticamente pueden recibir contexto y usarlo como variables en sus consultas GraphQL. Para anular el valor predeterminado y pasar tu propio contexto, abre el archivo `gatsby-node.js` de tu sitio y agregua algo similar a lo siguiente:

```javascript:title=gatsby-node.js
exports.onCreatePage = ({ page, actions }) => {
  const { createPage, deletePage } = actions

  deletePage(page)
  // Puedes acceder a la variable "house" en las consultas de su página ahora
  createPage({
    ...page,
    context: {
      ...page.context,
      house: `Gryffindor`,
    },
  })
}
```

En tus páginas y plantillas, puedes acceder a su contexto a través de la prop `pageContext` como este:

```jsx
import React from "react"

const Page = ({ pageContext }) => {
  return <div>{pageContext.house}</div>
}

export default Page
```

El contexto de la página se serializa antes de pasar a las páginas: esto significa que no se puede usar para pasar funciones a los componentes.

## Crear rutas solo para clientes

En casos específicos, es posible que desees crear un sitio con porciones exclusivas para clientes que se cierran mediante autenticación. Para obtener más información sobre cómo lograr esto, consulta [client-only routes & user authentication](https://www.gatsbyjs.org/docs/client-only-routes-and-user-authentication/).
