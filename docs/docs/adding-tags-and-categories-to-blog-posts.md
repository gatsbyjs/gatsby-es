---
title: Creación de Páginas de Etiquetas para Publicaciones de Blog
---

Crear páginas de etiquetas para tu publicación de blog es una forma de permitir a los visitantes navegar por contenido relacionado.

Para agregar etiquetas a las publicaciones de tu blog, primero deberás configurar tu sitio para convertir tus páginas _markdown_ en publicaciones de blog. Para configurar las páginas de tu blog, mira el [tutorial de la capa de datos de Gatsby](/tutorial/part-four/) y [Agregar Páginas en _Markdown_](/docs/adding-markdown-pages/).

El proceso esencialmente se verá así:

1.  Agregar etiquetas a tus archivos `markdown`
2.  Escribir una consulta para obtener todas las etiquetas para tus publicaciones
3.  Hacer una página plantilla de etiquetas (para `/tags/{tag}`)
4.  Modificar `gatsby-node.js` para renderizar páginas usando la plantilla
5.  Hacer una página _index_ de etiquetas (`/tags`) que renderice una lista de todas las etiquetas
6.  _(opcional)_ Renderizar etiquetas dentro de tus publicaciones de blog

## Agregar etiquetas a tus archivos `markdown`

Agregas etiquetas definiéndolas en el `frontmatter` de tu archivo _Markdown_. El `frontmatter` es el área en la parte superior rodeada de guiones que incluye datos de publicaciones como el título y la fecha.

```md
---
title: "Un viaje al zoológico"
---

Fui al zoológico hoy. Fue terrible.
```

Los campos pueden ser cadenas de texto, números, o arreglos. Como una publicación generalmente puede tener muchas etiquetas, tiene sentido definirla como un arreglo. Aquí agregamos nuestro nuevo campo de etiquetas:

```md
---
title: "Un viaje al zoológico"
tags: ["animales", "Chicago", "zoológicos"]
---

Fui al zoológico hoy. Fue terrible.
```

Si `gatsby develop` está corriendo, reinícialo para que Gatsby pueda utilizar los nuevos campos.

## Escribir una consulta para obtener todas las etiquetas para tus publicaciones

Ahora, estos campos están disponibles en la capa de datos. Para usar datos de un campo, consúltalo usando `graphql`. Todos los campos están disponibles para consultar dentro de `frontmatter`

Intenta correr la siguiente consulta en Graph<em>i</em>QL (`localhost:8000/___graphql`):

```graphql
{
  allMarkdownRemark {
    group(field: frontmatter___tags) {
      tag: fieldValue
      totalCount
    }
  }
}
```

La consulta anterior agrupa las publicaciones por `tags`, y retorna cada `tag` con el número de publicaciones como `totalCount`. Además, podríamos extraer algunos datos de publicaciones en cada grupo si es necesario. Para mantener este tutorial pequeño, solo estamos usando el nombre de la etiqueta en nuestras páginas de etiquetas. Hagamos la página plantilla de etiquetas ahora:

## Hacer una página plantilla de etiquetas (para `/tags/{tag}`)

Si seguiste el tutorial para [Agregar Páginas en _Markdown_](/docs/adding-markdown-pages/), entonces este proceso debería sonar familiar: haremos una página plantilla de etiquetas, luego la usaremos en `createPages` en `gatsby-node.js` para generar páginas individuales para las etiquetas en nuestras publicaciones.

Primero, agregaremos una plantilla de etiquetas en `src/templates/tags.js`:

```jsx:title=src/templates/tags.js
import React from "react"
import PropTypes from "prop-types"

// Componentes
import { Link, graphql } from "gatsby"

const Tags = ({ pageContext, data }) => {
  const { tag } = pageContext
  const { edges, totalCount } = data.allMarkdownRemark
  const tagHeader = `${totalCount} post${
    totalCount === 1 ? "" : "s"
  } tagged with "${tag}"`

  return (
    <div>
      <h1>{tagHeader}</h1>
      <ul>
        {edges.map(({ node }) => {
          const { slug } = node.fields
          const { title } = node.frontmatter
          return (
            <li key={slug}>
              <Link to={slug}>{title}</Link>
            </li>
          )
        })}
      </ul>
      {/*
              Esto enlaza a una página que aún no existe.
              ¡Volveremos a esto!
            */}
      <Link to="/tags">All tags</Link>
    </div>
  )
}

Tags.propTypes = {
  pageContext: PropTypes.shape({
    tag: PropTypes.string.isRequired,
  }),
  data: PropTypes.shape({
    allMarkdownRemark: PropTypes.shape({
      totalCount: PropTypes.number.isRequired,
      edges: PropTypes.arrayOf(
        PropTypes.shape({
          node: PropTypes.shape({
            frontmatter: PropTypes.shape({
              title: PropTypes.string.isRequired,
            }),
            fields: PropTypes.shape({
              slug: PropTypes.string.isRequired,
            }),
          }),
        }).isRequired
      ),
    }),
  }),
}

export default Tags

export const pageQuery = graphql`
  query($tag: String) {
    allMarkdownRemark(
      limit: 2000
      sort: { fields: [frontmatter___date], order: DESC }
      filter: { frontmatter: { tags: { in: [$tag] } } }
    ) {
      totalCount
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

**Nota**: los `propTypes` están incluidos en este ejemplo para ayudarte a asegurar que estás obteniendo todos los datos que necesitas en el componente, y sirven como una guía mientras desestructuras / usas estas _props_.

## Modificar `gatsby-node.js` para renderizar páginas usando la plantilla

Ahora tenemos una plantilla. ¡Excelente! Asumiré que seguiste el tutorial para [Agregar Páginas en _Markdown_](/docs/adding-markdown-pages/) y tienes un ejemplo de `createPages` que genera páginas de publicación, así como páginas de etiquetas. En el archivo del sitio `gatsby-node.js`, incluye `lodash` (`const _ = require('lodash')`) y luego asegúrate que tu [`createPages`](/docs/node-apis/#createPages) se parezca a esto:

```js:title=gatsby-node.js
const path = require("path")
const _ = require("lodash")

exports.createPages = async ({ actions, graphql, reporter }) => {
  const { createPage } = actions

  const blogPostTemplate = path.resolve("src/templates/blog.js")
  const tagTemplate = path.resolve("src/templates/tags.js")

  const result = await graphql(`
    {
      postsRemark: allMarkdownRemark(
        sort: { order: DESC, fields: [frontmatter___date] }
        limit: 2000
      ) {
        edges {
          node {
            fields {
              slug
            }
            frontmatter {
              tags
            }
          }
        }
      }
      tagsGroup: allMarkdownRemark(limit: 2000) {
        group(field: frontmatter___tags) {
          fieldValue
        }
      }
    }
  `)

  // manejar errores
  if (result.errors) {
    reporter.panicOnBuild(`Error while running GraphQL query.`)
    return
  }

  const posts = result.data.postsRemark.edges

  // Crear páginas de detalles de publicaciones
  posts.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: blogPostTemplate,
    })
  })

  // Extraer datos de etiquetas de la consulta
  const tags = result.data.tagsGroup.group

  // Hacer páginas de etiquetas
  tags.forEach(tag => {
    createPage({
      path: `/tags/${_.kebabCase(tag.fieldValue)}/`,
      component: tagTemplate,
      context: {
        tag: tag.fieldValue,
      },
    })
  })
}
```

Algunas notas:

- Nuestra consulta GraphQL solo busca datos que necesitamos para generar estas páginas. Cualquier otra cosa puede ser consultada nuevamente más tarde (y, si te das cuenta, hacemos esto arriba en la plantilla de etiquetas para el título de la publicación).
- Hemos hecho referencia a dos campos `allMarkdownRemark` en nuestra consulta. Para evitar colisiones de nombres debemos asignar un [alias](/docs/graphql-reference/#aliasing) a uno de ellos. Hemos asignado un alias a ambos campos para que nuestro código sea más legible para los humanos.
- Al hacer las páginas de etiquetas, ten en cuenta que pasamos `tag.name` a través del `context`. Este es el valor que se usa en la consulta `TagPage` para limitar nuestra búsqueda a solo publicaciones etiquetadas con la etiqueta en la URL.

## Hacer una página _index_ de etiquetas (`/tags`) que renderice una lista de todas las etiquetas

Nuestra página `/tags` simplemente listará todas las etiquetas, seguidas por el número de publicaciones con dicha etiqueta. Podemos obtener los datos con la primera consulta que escribimos anteriormente, que agrupa publicaciones por etiquetas:

```jsx:title=src/pages/tags.js
import React from "react"
import PropTypes from "prop-types"

// Utilidades
import kebabCase from "lodash/kebabCase"

// Componentes
import { Helmet } from "react-helmet"
import { Link, graphql } from "gatsby"

const TagsPage = ({
  data: {
    allMarkdownRemark: { group },
    site: {
      siteMetadata: { title },
    },
  },
}) => (
  <div>
    <Helmet title={title} />
    <div>
      <h1>Tags</h1>
      <ul>
        {group.map(tag => (
          <li key={tag.fieldValue}>
            <Link to={`/tags/${kebabCase(tag.fieldValue)}/`}>
              {tag.fieldValue} ({tag.totalCount})
            </Link>
          </li>
        ))}
      </ul>
    </div>
  </div>
)

TagsPage.propTypes = {
  data: PropTypes.shape({
    allMarkdownRemark: PropTypes.shape({
      group: PropTypes.arrayOf(
        PropTypes.shape({
          fieldValue: PropTypes.string.isRequired,
          totalCount: PropTypes.number.isRequired,
        }).isRequired
      ),
    }),
    site: PropTypes.shape({
      siteMetadata: PropTypes.shape({
        title: PropTypes.string.isRequired,
      }),
    }),
  }),
}

export default TagsPage

export const pageQuery = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
    allMarkdownRemark(limit: 2000) {
      group(field: frontmatter___tags) {
        fieldValue
        totalCount
      }
    }
  }
`
```

## _(opcional)_ Renderizar etiquetas dentro de tus publicaciones de blog

¡Un esfuerzo final! En cualquier otro lugar donde desees renderizar tus etiquetas, simplemente agrégalas a la sección `frontmatter` de tu consulta `graphql` y accede a ellas en tu componente como cualquier otro _prop_.
