---
title: Agregar paginación
---

Una página que muestra una lista de contenido se alarga a medida que aumenta la cantidad de contenido.
La paginación es la técnica de difundir ese contenido en varias páginas.

El objetivo de la paginación es crear varias páginas (desde un único [template](/docs/building-with-components/#page-template-components)) que muestran un número limitado de elementos.

Cada página [query GraphQL](/docs/querying-with-graphql/) para esos elementos específicos.

La información necesaria para consultar esos elementos específicos (es decir, valores para [`limit`](/docs/graphql-reference/#limit) y [`skip`](/docs/graphql-reference/#skip)) vendrá de la [`context`](/docs/graphql-reference/#query-variables) que se agrega cuando [crear páginas](/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) en `gatsby-node`.

### Ejemplo

```js:title=src/templates/blog-list-template.js
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

El código anterior creará una cantidad de páginas que se basa en el número total de publicaciones. Cada página mostrará una lista `postsPerPage`(6) , hasta que haya menos de `postsPerPage`(6) puestos a la izquierda.
La ruta de la primera página es `/blog`, siguientes páginas tendrán una ruta del formulario: `/blog/2`, `/blog/3`, etc.

### Otros recursos

- Sigue esto [tutorial paso a paso](https://nickymeuleman.netlify.com/blog/gatsby-pagination/) para agregar enlaces a la página anterior/siguiente y la navegación tradicional de la página en la parte inferior de la página

- ¿Ves [gatsby-paginated-blog](https://github.com/NickyMeuleman/gatsby-paginated-blog) [(demo)](https://nickymeuleman.github.io/gatsby-paginated-blog/) para una extensión de la [gatsby-starter-blog](https://github.com/gatsbyjs/gatsby-starter-blog) with pagination in place
