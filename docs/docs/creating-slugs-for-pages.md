---
title: Creando Slugs para páginas
---

La lógica para crear slugs a partir de nombres de archivos puede ser complicada, el plugin `gatsby-source-filesystem` viene con una función para crearlos.

## Instalación

`npm install --save gatsby-source-filesystem`

## Crear slugs en gatsby-node.js

Agrega tus nuevos slugs directamente en los nodos `MarkdownRemark`. Todos los datos que agregues a los nodos están disponibles para consultarlos más tarde con GraphQL.

Para hacerlo, utilizarás una función pasada a nuestra implementación de API llamada [`createNodeField`](/docs/actions/#createNodeField). Esta función te permite crear campos adicionales en los nodos creados por otros plugins.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)

// highlight-start
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  // highlight-end
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
    // highlight-end
  }
}
```

## Slugs creados por consultas

Abre y actualiza GraphiQL, luego ejecuta esta consulta GraphQL para ver todas tus slugs:

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        fields {
          slug
        }
      }
    }
  }
}
```
