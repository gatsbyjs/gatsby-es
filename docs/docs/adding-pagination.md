---
title: Agregar paginación
---

Una página que muestra una lista de contenido se hace más larga a medida que aumenta la cantidad de contenido.
La paginación es la técnica de esparcir ese contenido a lo largo de varias páginas.

El objetivo de la paginación es crear varias páginas (a partir de una única [plantilla](/docs/building-with-components/#page-template-components)) que contengan un número limitado de entradas.

Cada página realizará [una consulta con GraphQL](/docs/querying-with-graphql/) para esas entradas en concreto.

La información necesaria para buscar esas entradas en concreto (es decir, los valores de [`limit`](/docs/graphql-reference/#limit) y [`skip`](/docs/graphql-reference/#skip)) provendrán del [`context`](/docs/graphql-reference/#query-variables) que se añade cuando se [crean páginas](/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) en `gatsby-node`.

### Ejemplos

```jsx:title=src/templates/blog-list-template.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default class BlogList extends React.Component {
  render() {
    const posts = this.props.data.allMarkdownRemark.edges
    return (
      <Layout>
        {posts.map(({ node }) => {
          const title = node.frontmatter.title || node.fields.slug
          return <div key={node.fields.slug}>{title}</div>
        })}
      </Layout>
    )
  }
}

export const blogListQuery = graphql`
// highlight-start
  query blogListQuery($skip: Int!, $limit: Int!) {
    allMarkdownRemark(
      sort: { fields: [frontmatter___date], order: DESC }
      limit: $limit
      skip: $skip
    ) {
// highlight-end
      edges {
        node {
          fields {
            slug
          }
          frontmatter {
            title
          }
        }
      }
    }
  }
`
```

```js:title=gatsby-node.js
const path = require("path")
const { createFilePath } = require("gatsby-source-filesystem")

exports.createPages = async ({ graphql, actions, reporter }) => {
  const { createPage } = actions

  const result = await graphql(
    `
      {
        allMarkdownRemark(
          sort: { fields: [frontmatter___date], order: DESC }
          limit: 1000
        ) {
          edges {
            node {
              fields {
                slug
              }
            }
          }
        }
      }
    `
  )

  if (result.errors) {
    reporter.panicOnBuild(`Error while running GraphQL query.`)
    return
  }

  // ...

  // Create blog-list pages
  // highlight-start
  const posts = result.data.allMarkdownRemark.edges
  const postsPerPage = 6
  const numPages = Math.ceil(posts.length / postsPerPage)

  Array.from({ length: numPages }).forEach((_, i) => {
    createPage({
      path: i === 0 ? `/blog` : `/blog/${i + 1}`,
      component: path.resolve("./src/templates/blog-list-template.js"),
      context: {
        limit: postsPerPage,
        skip: i * postsPerPage,
        numPages,
        currentPage: i + 1,
      },
    })
  })
  // highlight-end
}

exports.onCreateNode = ({ node, actions, getNode }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const value = createFilePath({ node, getNode })
    createNodeField({
      name: `slug`,
      node,
      value,
    })
  }
}
```

El código anterior creará una cierta cantidad de páginas que se calculará en función del número total de entradas. Cada página listará (6) entradas `postsPerPage`, hasta que existan menos de (6) entradas `postsPerPage`.
La dirección para la primera página es `/blog`, las siguientes páginas tendrán una dirección de la forma: `/blog/2`, `/blog/3`, etc.

### Otros recursos

- Sigue este [tutorial paso a paso](https://nickymeuleman.netlify.com/blog/gatsby-pagination/) para agregar enlaces a la página anterior, página siguiente y a la navegación tradicional de la página ubicada en la parte inferior de la página.

- Mira la [(demo)](https://nickymeuleman.github.io/gatsby-paginated-blog/) de [gatsby-paginated-blog](https://github.com/NickyMeuleman/gatsby-paginated-blog) para una ampliación del [gatsby-starter-blog](https://github.com/gatsbyjs/gatsby-starter-blog) oficial con paginación implementada.
