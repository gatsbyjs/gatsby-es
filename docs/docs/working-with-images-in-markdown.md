---
title: Trabajando con imágenes en publicaciones y páginas de Markdown
---

Al crear sitios Gatsby compuestos principalmente por páginas o publicaciones de Markdown, la inserción de imágenes puede mejorar el contenido. Agregar imágenes se puede hacer de múltiples maneras.

## Imágenes destacadas con metadatos de Frontmatter

En sitios como un blog, es posible que desees incluir una imagen destacada que aparece en la parte superior de una página. Una forma de hacerlo es tomar el nombre de archivo de la imagen de un campo de _frontmatter_ y luego transformarlo con `gatsby-plugin-sharp` en una consulta GraphQL.

Esta solución supone que ya tienes páginas generadas mediante programación desde Markdown con procesadores como `gatsby-transformer-remark` o `gatsby-plugin-mdx`. De lo contrario, lee hasta la [Parte 7 del Tutorial de Gatsby](/tutorial/part-seven/). Esto será la base del tutorial y, como tal, se usará `gatsby-transformer-remark` para este ejemplo.

> Nota: Esto se puede hacer de manera similar usando también [MDX](/docs/mdx/). En lugar de los nodos `markdownRemark` en GraphQL, se pueden intercambiar por `Mdx` y debería funcionar.

Para comenzar, descarga los _plugins_ para Gatsby-image como se menciona en [Uso de gatsby-image](/docs/using-gatsby-image/).

```shell
npm install --save gatsby-image gatsby-transformer-sharp gatsby-plugin-sharp
```

También querrás tener instalado `gatsby-source-filesystem`. Después, configura los diversos _plugins_ en el archivo `gatsby-config` .

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    `gatsby-transformer-sharp`,
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`,
      },
    },
  ],
}
```

Entonces, en un ejemplo de archivo markdown, añade un campo llamado `featuredImage`:

```md:title=src/pages/example-post.md
---
title: Mi Asombroso Post
featuredImage: ./awesome-image.png
---

¡El contenido va aquí!
```

El campo `featuredImage` debe incluir la ruta relativa de la imagen que deseas utilizar.

Ahora puedes consultar la imagen destacada en GraphQL. Si la ruta del archivo apunta a una imagen real, se transformará en un nodo `Archivo` en GraphQL y entonces podrás obtener los datos de la imagen utilizando el campo `childImageSharp`.

Esto se puede agregar a la consulta GraphQL en un archivo de plantilla Markdown. En este ejemplo, se utiliza una [consulta Fluid](/docs/gatsby-image#images-that-stretch-across-a-fluid-container) para hacer una imagen responsiva.

```jsx:title=src/templates/blog-post.js
export const query = graphql`
  query PostQuery($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
        // highlight-start
        featuredImage {
          childImageSharp {
            fluid(maxWidth: 800) {
              ...GatsbyImageSharpFluid
            }
          }
        }
        // highlight-end
      }
    }
  }
`
```

También en la plantilla de publicación Markdown, importa el paquete `gatsby-image` y pasa los resultados de la consulta graphQL a un componente` <Img /> `.

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
// highlight-start
import Img from "gatsby-image"
// highlight-end

export default ({ data }) => {
  let post = data.markdownRemark

  // highlight-start
  let featuredImgFluid = post.frontmatter.featuredImage.childImageSharp.fluid
  // highlight-end

  return (
    <Layout>
      <div>
        <h1>{post.frontmatter.title}</h1>
        // highlight-start
        <Img fluid={featuredImgFluid} />
        // highlight-end
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query PostQuery($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
        featuredImage {
          childImageSharp {
            fluid(maxWidth: 800) {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`
```

Tu imagen destacada debería aparecer ahora en la página generada justo debajo del encabezado principal. ¡Tachán!

## Imágenes en línea con `gatsby-remark-images`

Las imágenes también pueden incluirse en el propio cuerpo de Markdown. El plugin [gatsby-remark-images](/packages/gatsby-remark-images) es útil para esto.

Comienza instalando `gatsby-remark-images` y `gatsby-plugin-sharp`.

```shell
npm install --save gatsby-remark-images gatsby-plugin-sharp
```

También asegúrate de que esté instalado `gatsby-source-filesystem` y apunte al directorio donde se encuentran tus imágenes.

Configura los _plugins_ en tu archivo `gatsby-config`. Al igual que con el ejemplo anterior, se pueden usar tanto `Remark` como `MDX`; `gatsby-plugin-mdx` será usado en este caso. Coloca el _plugin_ `gatsby-remark-images` dentro del campo de opciones `gatsbyRemarkPlugins` de `gatsby-plugin-mdx`.

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-sharp`,
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        gatsbyRemarkPlugins: [
          {
            resolve: `gatsby-remark-images`,
            options: {
              maxWidth: 1200,
            },
          },
        ],
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`,
      },
    },
  ],
}
```

Con esta configuración, puedes usar la sintaxis predeterminada de Markdown para las imágenes. Sharp los procesará y aparecerán como si los hubiera colocado en un componente `gatsby-image`.

```md
![Imagen asombrosa](./my-awesome-image.png)
```
