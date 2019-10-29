---
title: Agregar una Lista de Posts de un Blog en Markdown
---

Una vez que hayas añadido páginas en _Markdown_ a tu sitio, estás a un solo paso de poder listar tus posts en una página índice dedicada.

### Creación de posts

Como es descrito [aquí](/docs/adding-markdown-pages), tendrás que crear tus posts en archivos _Markdown_, los cuales se verán algo así:

```md
---
path: "/blog/my-first-post"
date: "2017-11-07"
title: "My first blog post"
---

Has anyone heard about GatsbyJS yet?
```

### Creación de página

El primer paso será crear la página que mostrará tus posts en `src/pages/`.  Puedes usar `index.js` por ejemplo.

```jsx:title=src/pages/index.js
import React from "react"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // Puedes filtrar tus posts basados en algún criterio
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage
```

### Creación de la consulta GraphQL

En segundo lugar, necesitas proveer los datos a tu componente mediante una consulta GraphQL. La añadiremos de tal manera que `index.js`, se verá así:

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // Puedes filtrar tus posts basados en algún criterio
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage

export const pageQuery = graphql`
  query {
    allMarkdownRemark(sort: { order: DESC, fields: [frontmatter___date] }) {
      edges {
        node {
          id
          excerpt(pruneLength: 250)
          frontmatter {
            date(formatString: "MMMM DD, YYYY")
            path
            title
          }
        }
      }
    }
  }
`
```

### Creación del componente `PostLink`

La única tarea que queda por hacer es añadir el componente `PostLink`. Crea un nuevo archivo `post-link.js` en `src/components/` y añade lo siguiente:

```jsx:title=src/components/post-link.js
import React from "react"
import { Link } from "gatsby"

const PostLink = ({ post }) => (
  <div>
    <Link to={post.frontmatter.path}>
      {post.frontmatter.title} ({post.frontmatter.date})
    </Link>
  </div>
)

export default PostLink
```

Esto debería mostrarte una página con tus posts ordenados por fecha de manera descendente. ¡Puedes personalizar aún más el `frontmatter` y los componentes de página y `PostLink` para obtener los efectos que desees!
