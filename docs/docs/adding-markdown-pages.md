---
title: Añadiendo páginas de Markdown
---

Gatsby puede usar archivos de Markdown para crear páginas en tu sitio.
Añades plugins para leer y comprender carpetas con archivos Markdown y desde ellos crear páginas automáticamente.

Aquí estan los pasos que Gatsby sigue para hacer esto posible.

1.  Leer archivos en Gatsby desde el sistema de archivos
2.  Transformar Markdown a HTML y [frontmatter](#frontmatter-para-metadatos-en-markdown-files) a datos
3.  Añade un archivo Markdown
4.  Crea un componente de página para los archivos de Markdown
5.  Crea páginas estáticas usando `createPage` de la API en Node.js de Gatsby

## Lee archivos en Gatsby desde el sistema de archivos

Usa el plugin [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/#gatsby-source-filesystem) para leer archivos.

#### Instalar

`npm install --save gatsby-source-filesystem`

#### Añadir plugin

**NOTA:** Hay dos formas para añadir un plugin en `gatsby-config.js`. Puedes pasar un string con el nombre del plugin o en caso de que quieras incluir opciones, pasar un objeto.

Abre `gatsby-config.js` para añadir el plugin `gatsby-source-filesystem`. Ahora pasa el objeto desde el siguiente bloque al array de `plugins`. Pasando un objeto que incluye la clave `path`, estableces la ruta del sistema de archivos.

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-source-filesystem`,
    options: {
      name: `markdown-pages`,
      path: `${__dirname}/src/markdown-pages`,
    },
  },
]
```

Completando los pasos anteriores significa que "obtienes" los archivos de Markdown del sistema de archivos. Ahora puedes "transformar" los archivos de Markdown a HTML y los _frontmatter_ de YAML a JSON. 

### Transforma Markdown a HTML y frontmatter a datos usando `gatsby-transformer-remark`

Usarás el plugin [`gatsby-transformer-remark`](/packages/gatsby-transformer-remark/) para reconocer archivos que son Markdown y leer su contenido. El plugin convertirá en `frontmatter` la parte de metadatos _frontmatter_ de tus archivos Markdown y en HTML la parte de contenido. 

#### Instalar

`npm install --save gatsby-transformer-remark`

#### Añadir plugin

Añade esto a `gatsby-config.js` después de lo añadido anteriormente `gatsby-source-filesystem`.

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-source-filesystem`,
    options: {
      path: `${__dirname}/src/markdown-pages`,
      name: `markdown-pages`,
    },
  },
  `gatsby-transformer-remark`,
]
```

### Añadir un archivo Markdown

Crea una carpeta en el directorio `/src` de tu aplicación Gatsby llamado `markdown-pages`.
Ahora crea un archivo Markdown dentro de él con el nombre `post-1.md`.

#### Frontmatter para metadatos en markdown files

Cuando creas un archivo Markdown, puedes incluir un conjunto de parejas clave-valor que pueden ser usadas para aportar datos adicionales relevantes para especificar páginas en la capa de datos de GraphQL. Este dato es llamado _frontmatter_ y está denotado por tres guiones al principio y final del bloque. Este bloque será analizado por `gatsby-transformer-remark` como `frontmatter`. La API GraphQL proveerá las parejas clave-valor como datos en nuestros componentes de React. 

```markdown:title=src/markdown-pages/post-1.md
---
path: "/blog/my-first-post"
date: "2019-05-04"
title: "Mi primer post del blog"
---
```

Lo que es importante en este paso es la pareja con clave `path`. El valor que es asignado a la clave `path` es usado para navegarlo hacia tu publicación.

### Crear un template de página para archivos de Markdown

Crea una carpeta en el directorio `/src` de tu aplicación Gatsby llamado `templates`.
Ahora crea un `blogTemplate.js` dentro de ella con el siguiente contenido:

```jsx:title=src/templates/blogTemplate.js
import React from "react"
import { graphql } from "gatsby"

export default function Template({
  data, // este prop será inyectado por la consulta GraphQL abajo.
}) {
  const { markdownRemark } = data // data.markdownRemark contiene nuestros datos del post 
  const { frontmatter, html } = markdownRemark
  return (
    <div className="blog-post-container">
      <div className="blog-post">
        <h1>{frontmatter.title}</h1>
        <h2>{frontmatter.date}</h2>
        <div
          className="blog-post-content"
          dangerouslySetInnerHTML={{ __html: html }}
        />
      </div>
    </div>
  )
}

export const pageQuery = graphql`
  query($path: String!) {
    markdownRemark(frontmatter: { path: { eq: $path } }) {
      html
      frontmatter {
        date(formatString: "MMMM DD, YYYY")
        path
        title
      }
    }
  }
`
```

Hay dos cosas importantes en el archivo superior:

1.  Una consulta GraphQL es realizada en la segunda mitad del archivo para obtener los datos de Markdown. Gatsby obtiene automáticamente todos los metadatos Markdown y HTML en el resultado de esta consulta.

    **Nota: Para aprender más sobre GraphQL, considera esta [excelente fuente](https://www.howtographql.com/)**

2.  El resultado de la consulta es inyectada por Gatsby en el componente `Template` como `data`. `markdownRemark` es la propiedad en la que encontrarás todos los detalles del archivo de Markdown. Puedes usarlo para construir un plantilla para la vista de nuestro post del blog. Como es un componente de React, podrías darle un estilo con cualquiera de los [sistemas de estilo recomendados](/docs/styling/) en Gatsby.

### Crear páginas estáticas usando `createPage` de la API en Node.js de Gatsby

Gatsby expone una poderosa API en Node.JS, la cual permite funcionalidades como la creación de páginas dinámicas. Esta API está disponible en el archivo `gatsby-node.js`  en el directorio raíz de tu proyecto, al mismo nivel de `gatsby-config.js`. Cada *export* encontrado en este archivo será ejecutado por Gatsby, como se detalla en su [especificación API Node](/docs/node-apis/). Sin embargo, sólo tienes que preocuparte por una API en particular de esta instancia, `createPages`.

Usa `graphql` para consultar el archivo Markdown como debajo. A continuación usa la acción creadora `createPage` para crear una página para cada uno de los archivos de Markdown usando el `blogTemplate.js` que has creado en el paso previo.

**NOTA:** Gatsby llama a la API `createPages`  (si está presente) en tiempo de compilación con parámetros inyectados, `actions` y `graphql`.

```javascript:title=gatsby-node.js
const path = require(`path`)

exports.createPages = async ({ actions, graphql, reporter }) => {
  const { createPage } = actions

  const blogPostTemplate = path.resolve(`src/templates/blogTemplate.js`)

  const result = await graphql(`
    {
      allMarkdownRemark(
        sort: { order: DESC, fields: [frontmatter___date] }
        limit: 1000
      ) {
        edges {
          node {
            frontmatter {
              path
            }
          }
        }
      }
    }
  `)

  // Manejo de errores
  if (result.errors) {
    reporter.panicOnBuild(`Error ejecutando consulta GraphQL.`)
    return
  }

  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.frontmatter.path,
      component: blogPostTemplate,
      context: {}, // datos adicionales pueden ser pasados vía contexto
    })
  })
}
```

Esto debería de ayudarte a comenzar con algo de funcionalidad básica de Markdown en tu sitio Gatbsy. ¡Puedes personalizar el _frontmatter_ y la plantilla de archivo para obtener los efectos deseados!

Para más información, echa un vistazo al ejemplo en funcionamiento `using-markdown-pages`. Puedes encontrarlo en la [Sección de ejemplos de Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/examples).

## Otros tutoriales

Revisa los tutoriales listados en la página de [Awesome Gatsby](/docs/awesome-gatsby-resources/#gatsby-tutorials) para más información sobre como crear sitios con Gatsby y Markdown. 

## Gatsby Markdown starters

Hay también un número de [Gatsby starters](/starters?c=Markdown) que vienen preconfigurados para trabajar con Markdown.
