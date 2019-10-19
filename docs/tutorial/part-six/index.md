---
title: Plugins Transformadores
typora-copy-images-to: ./
disableTableOfContents: true
---

> Este tutorial es parte de una serie sobre la capa de datos de Gatsby. Asegúrate de haber visto [parte 4](/tutorial/part-four/) y [parte 5](/tutorial/part-five/) antes de continuar aquí.

## ¿Qué hay en este tutorial?

El tutorial anterior mostró cómo los plugins de origen aportan datos _dentro_ del sistema de datos de Gatsby. En este tutorial, aprenderá como los plugins transformadores _transforman_ el contenido en bruto aportado por los plugins de origen. La combinación de los plugins de origen y plugins transformadores puede manejar todo el abastecimiento y transformación de datos que pueda necesitar al crear un sitio de Gatsby.

## Plugins Transformadores

A menudo, el formato de datos que obtiene de los plugins de origen no
es lo que desea utilizar para construir su sitio web. El plugin de sistema
de archivos le permite consultar datos _sobre_ archivos pero ¿y si quiere
consultar datos _dentro_ de los archivos?

Para que esto sea posible, Gatsby soporta plugins transformadores que
toman contenido sin procesar de los plugins de origen y lo _transforman_ en
algo más útil.

Por ejemplo, archivos markdown. Es bueno escribir Markdown, pero
cuando construyes una página con él, necesitas que el Markdown sea HTML.

Agregue un archivo markdown a su sitio `src/pages/sweet-pandas-eating-sweets.md`
(Esta será su primer publicación de blog markdown) y aprenda cómo _transformarlo_ a HTML usando
plugins transformadores y GraphQL.

```markdown:title=src/pages/sweet-pandas-eating-sweets.md
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Pandas are really sweet.

Here's a video of a panda eating sweets.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

Una vez que guarde el archivo, mire nuevamente `/my-files/` el nuevo archivo markdown
está en la tabla. Esta es una característica muy poderosa de Gatsby. Como el ejemplo
anterior `siteMetadata`, los plugins de origen pueden recargar datos en vivo.
`gatsby-source-filesystem` siempre está buscando nuevos archivos para agregar y,
cuando los encuentra, vuelve a ejecutar sus consultas.

Agregue un plugin transformador que pueda transformar archivos markdown:

```shell
npm install --save gatsby-transformer-remark
```

Luego agréguelo a `gatsby-config.js` como de costumbre:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`, // highlight-line
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Reinicie el servidor de desarrollo, luego actualice (o abra de nuevo) GraphiQL
y busque en el autocompletado:

![markdown-autocomplete](markdown-autocomplete.png)

Seleccione `allMarkdownRemark` de nuevo y ejecutelo como lo hiciste para `allFile`.
Observará el archivo markdown que agregó recientemente. Explore los campos disponibles
en el nodo `MarkdownRemark`.

![markdown-query](markdown-query.png)

¡Okay! Con suerte, algunos conceptos básicos están comenzando a encajar.
Los plugins de origen aportan datos _dentro_ del sistemas de datos de Gatsby
y los _plugins transformadores_ transforma el contenido en bruto que aportan
los plugins de origen. Este patrón puede manejar todo el abastecimiento y
transformación de datos que pueda necesitar al crear un sitio de Gatsby.

## Cree una lista de los archivos markdown en `src/pages/index.js`

Ahora tendrá que crear una lista de sus archivos markdown en la portada.
Al igual que muchos blogs, desea terminar con una lista de enlaces en la página principal
que apunte a cada publicación del blog. Con GraphQL puede realizar una _consulta_
para obtener la lista actual de publicaciones markdown del blog, por lo que
no necesitará mantener la lista manualmente.

Al igual que con la página `src/pages/my-files.js`, reemplace `src/pages/index.js`
con lo siguiente para agregar una consulta GraphQL con un poco de HTML inicial y estilo.

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import { css } from "@emotion/core"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            <h3
              css={css`
                margin-bottom: ${rhythm(1 / 4)};
              `}
            >
              {node.frontmatter.title}{" "}
              <span
                css={css`
                  color: #bbb;
                `}
              >
                — {node.frontmatter.date}
              </span>
            </h3>
            <p>{node.excerpt}</p>
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

Ahora la portada debería lucir así:

![frontpage](frontpage.png)

But your one blog post looks a bit lonely. So let's add another one at
`src/pages/pandas-and-bananas.md`

```markdown:title=src/pages/pandas-and-bananas.md
---
title: "Pandas and Bananas"
date: "2017-08-21"
---

Do Pandas eat bananas? Check out this short video that shows that yes! pandas do
seem to really enjoy bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

![two-posts](two-posts.png)

¡Se ve genial! Excepto… el orden de las publicaciones es incorrecto.

Pero esto es fácil de arreglar. Al consultar una conexión de algún tipo,
puede pasar una variedad de argumentos a la consulta GraphQL. Puede `ordenar`
y `filtrar` nodos, establecer cuántos nodos `omitir` y elegir el `límite` de cuántos nodos recuperar.
Con este poderoso conjunto de operadores, puede seleccionar cualquier dato que desee,
en el formato que necesite.

En la consulta GraphQL de su página index, cambie `allMarkdownRemark` a
`allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC })`. _Nota: Hay 3 guiones bajos entre `frontmatter` y `date`._
Guarde esto y el orden de clasificación debe ser arreglado.

Intenta abrir GraphiQL y jugar con diferentes opciones de clasificación.
Puede ordenar la conexión `allFile` junto con otras conexiones.

Para obtener más documentación sobre nuestros operadores de consulta, explore nuestro [Guía de referencia de GraphQL.](/docs/graphql-reference/)

## Desafío

¡Intente crear una nueva página que contenga una publicación de blog y vea qué sucede con la lista de publicaciones de blog en la página de inicio!

## ¿Qué viene después?

¡Esto es genial! Acaba de crear una página de índice agradable donde está consultando
sus archivos markdown y producir una lista de títulos y extractos de publicaciones de blog.
Pero no solo quiere ver extractos, desea páginas reales para sus archivos markdown.

Puede continuar creando páginas colocando componentes React en `src/pages`. Sin embargo,
enseguida aprenderá como crear páginas _programaticamente_ a partir de los _datos_.
Gatsby _no_ esta limitado a hacer páginas a partir de archivos como muchos generadores
de sitios estáticos. Gatsby le permite utilizar GraphQL para consultar sus _datos_ y _mapear_
los resultados de la consulta a _páginas_, todo en tiempo de compilación.
Esta es una idea realmente poderosa. Explorarás sus implicaciones y formas de usarlo en el siguiente tutorial,
donde aprenderá como [crear programaticamente páginas a partir de los datos](/tutorial/part-seven/).
