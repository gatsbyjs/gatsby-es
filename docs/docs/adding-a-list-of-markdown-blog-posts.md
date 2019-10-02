---
title: Agregar una lista de entradas de blog Markdown
---

Una vez que haya agregado páginas de Markdown a su sitio, está a sólo un paso de ser capaz de publicar sus publicaciones en una página de índice dedicada.

### Creando publicaciones

Como se describe [aquí] (/docs/adding-markdown-pages), tendrá que crear sus publicaciones en archivos Markdown que se verán así:

```md
---
path: "/blog/my-first-post"
date: "2017-11-07"
title: "My first blog post"
---

¿Alguien ha oído hablar de GatsbyJS todavía?
```

### Creando la página

El primer paso será crear la página que mostrará sus publicaciones, en `src/pages/`. Por ejemplo, puede usar `index.js`.

```jsx:title=src/pages/index.js
import React from "react"
import PostLink from "../components/post-link"

const IndexPage = ({
  data: {
    allMarkdownRemark: { edges },
  },
}) => {
  const Posts = edges
    .filter(edge => !!edge.node.frontmatter.date) // You can filter your posts based on some criteria
    .map(edge => <PostLink key={edge.node.id} post={edge.node} />)

  return <div>{Posts}</div>
}

export default IndexPage
```

### Creando la consulta de GraphQL

En segundo lugar, debe proporcionar los datos a su componente con una consulta de GraphQL. Vamos a agregarlo, para que `index.js` se vea así:

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
    .filter(edge => !!edge.node.frontmatter.date) // You can filter your posts based on some criteria
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

### Creando el componente `PostLink`

Lo único que queda por hacer es agregar el componente `PostLink`. Cree un nuevo archivo `post-link.js` en `src/components/` y agregue lo siguiente:

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

Esto debería conseguirte una página con tus publicaciones ordenadas por fecha descendente. Puede personalizar aún más el `frontmatter` y los componentes de la página y `postlink` para obtener los efectos deseados!
