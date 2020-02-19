---
title: Crear páginas mediante programación a partir de datos
typora-copy-images-to: ./
disableTableOfContents: true
---

> Este tutorial es parte de una serie sobre la capa de datos de Gatsby. Asegúrate de haber visto [parte 4](/tutorial/part-four/), [parte 5](/tutorial/part-five/) y [part 6](/tutorial/part-six/) antes de continuar aquí.

## ¿Qué hay en este tutorial?

En el tutorial anterior, creaste una buena página index que consulta archivos
markdown y produce una lista de títulos de publicaciones de blog y extractos. Pero no solo quieres ver extractos, deseas páginas reales
para tus archivos markdown.

Puedes continuar creando páginas a través de componentes React en `src/pages`. Sin embargo, ahora
aprenderás cómo crear páginas a partir de _datos_ mediante _programación_. Gatsby _no_ se
limita a crear páginas a partir de archivos como muchos generadores de sitios estáticos. Gatsby te
permite utilizar GraphQL para consultar tus _datos_ y _mapear_ los resultados de la consulta a _páginas_, todo en
tiempo de compilación. Esta es una idea realmente poderosa. Explorarás sus implicaciones y
formas de usarlo durante el resto de esta parte del tutorial.

Comencemos.

## Crear slugs para páginas

Crear nuevas páginas tiene dos pasos:

1.  Generar la "ruta" o "slug" para la página.
2.  Crear la página.

_**Nota**: A menudo las fuentes de datos proporcionarán directamente un slug o nombre de ruta para el contenido — cuando trabajas con uno de esos sistemas (por ejemplo, un CMS), no necesitas crear slugs tu mismo como lo haces con los archivos markdown._

Para crear tus páginas markdown, aprenderás a utilizar dos API de Gatsby:
[`onCreateNode`](/docs/node-apis/#onCreateNode) y
[`createPages`](/docs/node-apis/#createPages). Estas son dos API caballos de batalla
que verás utilizadas en muchos sitios y plugins.

Hacemos todo lo posible para que las API de Gatsby sean simples de implementar. Para implementar un API, exporta una función
con el nombre del API desde `gatsby-node.js`.

Entonces, aquí es donde harás esto. En la raíz de tu sitio, crea un archivo llamado
`gatsby-node.js`. Luego agrega lo siguiente.

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type)
}
```

Gatsby llamará a esta función `onCreateNode` cada vez que se cree (o actualice) un nuevo nodo.

Detén y reinicia el servidor de desarrollo. Mientras lo haces, verás que algunos
nodos recién creados se registran en la consola de la terminal.

Usa esta API para agregar los slugs de tus páginas markdown a los
nodos `MarkdownRemark`.

Cambia tu función para que ahora solo registre nodos `MarkdownRemark`.

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  // highlight-start
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type)
  }
  // highlight-end
}
```

Quieres utilizar cada nombre de archivo markdown para crear el slug de la página. Para que
`pandas-and-bananas.md` se convierta en `/pandas-and-bananas/`. Pero, ¿cómo se obtiene
el nombre del archivo del nodo `MarkdownRemark`? Para obtenerlo, debes _atravesar_
el "grafo del nodo" hasta su nodo _padre_ `File`, ya que los nodos `File` contienen los datos que
necesitas sobre los archivos en el disco. Para hacer eso, modifica tu función nuevamente:

```javascript:title=gatsby-node.js
// highlight-next-line
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const fileNode = getNode(node.parent)
    console.log(`\n`, fileNode.relativePath)
    // highlight-end
  }
}
```

Después reinicia tu servidor de desarrollo, deberías ver las rutas relativas para que tus dos archivos
markdown se impriman en la pantalla del terminal.

![markdown-relative-path](markdown-relative-path.png)

Ahora tendrás que crear slugs. Como la lógica para crear slugs a partir de nombres de archivos puede ser
complicada, el plugin `gatsby-source-filesystem` se envía con una función para crear
slugs. Vamos a usar eso.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`) // highlight-line

exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` })) // highlight-line
  }
}
```

La función maneja la búsqueda del nodo padre `File` junto con la creación del
slug. Ejecuta el servidor de desarrollo nuevamente y deberías ver registrado en la terminal
dos slugs, uno para cada archivo markdown.

Ahora puedes agregar nuevos slugs directamente en los nodos `MarkdownRemark`. Esto es
poderoso, ya que cualquier información que agregues a los nodos está disponible para consultar más tarde con GraphQL.
Por lo tanto, será fácil obtener el slug cuando llegue el momento de crear las páginas.

Para hacerlo, usarás una función pasada a nuestra implementación de API llamada
[`createNodeField`](/docs/actions/#createNodeField). Esta función
te permite crear campos adicionales en nodos creados por otros plugins. Solo
el creador original de un nodo puede modificarlo directamente; todos los demás plugins
(incluido su `gatsby-node.js`) deben usar esta función para crear campos
adicionales.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)
// highlight-next-line
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions // highlight-line
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

Reinicia el servidor de desarrollo y abre o actualiza GraphiQL. Luego ejecuta
esta consulta GraphQL para ver tus nuevos slugs.

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

Ahora que se crearon los slugs, puedes crear las páginas.

## Crear páginas

En el mismo archivo `gatsby-node.js`, agrega lo siguiente.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

// highlight-start
exports.createPages = async ({ graphql, actions }) => {
  // **Nota:** La llamada a la función graphql devuelve una Promesa
  // consulta: https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Promise para más información
  const result = await graphql(`
    query {
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
  `)

  console.log(JSON.stringify(result, null, 4))
}
// highlight-end
```

Has agregado una implementación de
[`createPages`](/docs/node-apis/#createPages) API que Gatsby llama para que los plugins puedan agregar
páginas.

Como se menciona en la introducción de esta parte del tutorial, los pasos para crear páginas mediante programación son:

1.  Consultar datos con GraphQL
2.  Asignar los resultados de la consulta a páginas

El código anterior es el primer paso para crear páginas a partir de tu markdown, ya que estás
utilizando la función `graphql` suministrada para consultar los slugs markdown creados.
Luego, cierra la sesión del resultado de la consulta que debería verse así:

![query-markdown-slugs](query-markdown-slugs.png)

Necesitas una cosa adicional más allá de un slug para crear páginas: un componente de
plantilla de página. Como todo en Gatsby, las páginas programáticas funcionan con componentes
React. Al crear una página, debes especificar qué componente usar.

Crea un directorio en `src/templates`, y luego agrega lo siguiente en un archivo llamado
`src/templates/blog-post.js`.

```jsx:title=src/templates/blog-post.js
import React from "react"
import Layout from "../components/layout"

export default () => {
  return (
    <Layout>
      <div>Hola publicación de blog</div>
    </Layout>
  )
}
```

Luego actualiza `gatsby-node.js`

```javascript:title=gatsby-node.js
const path = require(`path`) // highlight-line
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions // highlight-line
  const result = await graphql(`
    query {
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
  `)

  // highlight-start
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/templates/blog-post.js`),
      context: {
        // Los datos pasados al contexto están disponibles
        // en consultas de página como variables GraphQL.
        slug: node.fields.slug,
      },
    })
  })
  // highlight-end
}
```

<<<<<<< HEAD
¡Reinicia el servidor de desarrollo y tus páginas serán creadas! Una manera fácil de
encontrar nuevas páginas que crees mientras desarrollas es ir a una ruta aleatoria donde
Gatsby te mostrará una lista de páginas en el sitio. Si vas a
<http://localhost:8000/sdf>, verás las nuevas páginas que creaste.
=======
Restart the development server and your pages will be created! An easy way to
find new pages you create while developing is to go to a random path where
Gatsby will helpfully show you a list of pages on the site. If you go to
`http://localhost:8000/sdf`, you'll see the new pages you created.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

![new-pages](new-pages.png)

Visita una de ellas y verás:

![hello-world-blog-post](hello-world-blog-post.png)

Lo cual es un poco aburrido y no es lo que quieres. Ahora puedes obtener datos de tu publicación markdown. Cambia
`src/templates/blog-post.js` a:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-start
export default ({ data }) => {
  const post = data.markdownRemark
  // highlight-end
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

// highlight-start
export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`
// highlight-end
```

Y…

![blog-post](blog-post.png)

¡Genial!

El último paso es vincular tus nuevas páginas desde la página de índice.

Regresa a `src/pages/index.js`, consulta tus slugs markdown, y crea
enlaces.

```jsx:title=src/pages/index.js
import React from "react"
import { css } from "@emotion/core"
import { Link, graphql } from "gatsby" // highlight-line
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Pandas increíbles comiendo cosas
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            {/* highlight-start */}
            <Link
              to={node.fields.slug}
              css={css`
                text-decoration: none;
                color: inherit;
              `}
            >
              {/* highlight-end */}
              <h3
                css={css`
                  margin-bottom: ${rhythm(1 / 4)};
                `}
              >
                {node.frontmatter.title}{" "}
                <span
                  css={css`
                    color: #555;
                  `}
                >
                  — {node.frontmatter.date}
                </span>
              </h3>
              <p>{node.excerpt}</p>
            </Link> {/* highlight-line */}
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC }) {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          // highlight-start
          fields {
            slug
          }
          // highlight-end
          excerpt
        }
      }
    }
  }
`
```

¡Y ahi tienes! Un blog de trabajo, aunque pequeño.

## Desafío

<<<<<<< HEAD
Intenta jugar más con el sitio. Intenta agregar más archivos markdown. Explora
consultando otros datos desde los nodos `MarkdownRemark` y agregandolos a las páginas de
portada o blog.
=======
Try playing more with the site. Try adding some more markdown files. Explore
querying other data from the `MarkdownRemark` nodes and adding them to the
front page or blog posts pages.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

En esta parte del tutorial, has aprendido los fundamentos de construir con
la capa de datos de Gatsby. Aprendiste como _origen_ y _transformar_ datos utilizando
plugins, cómo usar GraphQL para _mapear_ datos a páginas, y luego cómo construir _componentes
de plantilla de página_ donde consultas datos para cada página.

## ¿Qué viene después?

Ahora que has creado un sitio de Gatsby, ¿a dónde irás?

- ¡Comparte tu sitio de Gatsby en Twitter y ve lo que otras personas han creado al buscar #gatsbytutorial! Asegúrate de mencionar @gatsbyjs en tu Tweet e incluye el hashtag #gatsbytutorial :)
- Podrías echar un vistazo a algunos [ejemplos de sitios](https://github.com/gatsbyjs/gatsby/tree/master/examples#gatsby-example-websites)
- Explorar más [plugins](/docs/plugins/)
- Observar lo que [otras personas están construyendo con Gatsby](/showcase/)
- Revisar la documentación en [API de Gatsby](/docs/api-specification/), [nodos](/docs/node-interface/), o [GraphQL](/docs/graphql-reference/)