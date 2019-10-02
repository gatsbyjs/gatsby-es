---
title: Agregar una fuente RSS
---

## ¿Qué es una fuente RSS?

Un [Fuente RSS](https://en.wikipedia.org/wiki/RSS) es un archivo XML estándar que enumera el contenido de un sitio web en un formato de suscripción, lo que permite a los lectores consumir su contenido en agregadores de noticias, también llamados aplicaciones de lector de feeds.

Piense en ello como un canal de distribución sindicado para el contenido de su sitio.

## Instalar

Para generar una fuente RSS, puede usar el comando [`gatsby-plugin-feed`](/packages/gatsby-plugin-feed/) El paquete incluye: Para instalar este paquete, ejecute el siguiente comando:

```shell
npm install --save gatsby-plugin-feed
```

## Modo de empleo [gatsby-plugin-feed](/packages/gatsby-plugin-feed/)

Una vez completada la instalación, ahora puede agregar este plugin al archivo de configuración de su sitio, así:

```js:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    siteUrl: `https://www.example.com`,
  },
  plugins: [`gatsby-plugin-feed`],
}
```

Aquí hay un ejemplo de cómo podría implementar este complemento con Markdown, pero para otras fuentes, necesitará una forma de identificar de forma única el contenido, generalmente una URL o una babosa.

```js:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, actions, getNode }) => {
  const { createNodeField } = actions
  // highlight-next-line
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

Siguiente ejecutar una compilación (`npm run build`) ya que la generación de fuentes RSS solo ocurrirá para compilaciones de producción. De forma predeterminada, la ruta de la fuente RSS generada es `/rss.xml`, pero el plugin expone opciones para configurar esta funcionalidad predeterminada.

Para configuraciones básicas con contenido Markdown como el [gatsby-Arrancador-blog](https://github.com/gatsbyjs/gatsby-starter-blog), ¡Eso es todo lo que necesitas! Sin embargo, puede crear un esquema de fuente RSS personalizado usando código personalizado en sus archivos `gatsby-node.js `y `gatsby-config.js`.

## Personalización del plugin RSS

Es posible que su contenido no encaje perfectamente en el escenario de inicio de blogs, por varias razones como:

- Tu contenido no está en Markdown, por lo que el plugin no lo sabe
- Sus archivos Markdown tienen fechas en los nombres de archivo, para los cuales las URL slug causan 404s

La buena noticia es que puede acomodar estos escenarios y más en `gatsby-config.js `y `gatsby-node.js`.

Para personalizar el esquema de alimentación predeterminado (también conocido como estructura) del complemento para que funcione con el contenido de su sitio web, puede comenzar con el siguiente código:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-feed`,
      options: {
        query: `
          {
            site {
              siteMetadata {
                title
                description
                siteUrl
                site_url: siteUrl
              }
            }
          }
        `,
        feeds: [
          {
            /* highlight-start */
            serialize: ({ query: { site, allMarkdownRemark } }) => {
              return allMarkdownRemark.edges.map(edge => {
                /* highlight-end */
                return Object.assign({}, edge.node.frontmatter, {
                  description: edge.node.excerpt,
                  date: edge.node.frontmatter.date,
                  url: site.siteMetadata.siteUrl + edge.node.fields.slug,
                  guid: site.siteMetadata.siteUrl + edge.node.fields.slug,
                  custom_elements: [{ "content:encoded": edge.node.html }],
                })
              })
            },
            query: `
              {
                // highlight-next-line
                allMarkdownRemark(
                  sort: { order: DESC, fields: [frontmatter___date] },
                ) {
                  edges {
                    node {
                      excerpt
                      html
                      fields { slug }
                      frontmatter {
                        title
                        date
                      }
                    }
                  }
                }
              }
            `,
            output: "/rss.xml",
            title: "Your Site's RSS Feed",
          },
        ],
      },
    },
  ],
}
```

Este fragmento contiene una configuración personalizada de `gatsby-plugin-feed` en `gatsby-config.js` para consultar metadatos de su sitio, como su `title` y `siteURL`. También incluye una matriz `feeds` con al menos un objeto que contiene una consulta GraphQL y el método `serialize`, que le permite generar una estructura de fuente RSS personalizada. En este ejemplo, el contenido RSS proviene de archivos Markdown procedentes de su sitio y consultados con la clave `AllMarkdownRemark` y sus filtros y campos asociados.

El campo `output `en su objeto feed le permite personalizar el nombre de archivo de su fuente RSS, y `title` para el nombre de la fuente RSS de su sitio.

De forma predeterminada, se hace referencia a la fuente en todas las páginas. Puede personalizar este comportamiento proporcionando un campo adicional `match` del tipo `string`. Esta cadena se utilizará para construir un `RegExp`, y esta expresión regular se utilizará para probar el `nombre_ruta` de la página actual. Sólo las páginas que cumplan con la expresión regular tendrán la referencia de alimentación incluida.

Para ver su feed en acción, ejecute `gatsby build && gatsby serve` y luego puede inspeccionar el contenido y las URL en su archivo RSS en `http://localhost:9000/rss.xml`.

> NOTA: si tu blog tiene enlaces permanentes personalizados, como enlaces con o sin fechas en ellos, es posible que tengas que [customize `gatsby-node.js`](https://github.com/gatsbyjs/gatsby-starter-blog/blob/master/gatsby-node.js#L57) para generar las URL correctas en su fuente RSS. [Get in touch with us](/contributing/how-to-contribute/) si necesitas ayuda!

## Sintaxis para bloques RSS de iTunes

Si crea una fuente RSS para un podcast, probablemente querrá incluir bloques RSS de iTunes. Toman el formato de `itunes:author` que GraphQL no lee. Aquí hay un ejemplo de cómo implementar bloques RSS de iTunes usando este plugin:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-feed`,
      options: {
        query: `
          {
            site {
              siteMetadata {
                title
                description
                siteUrl
                site_url: siteUrl
              }
            }
          }
        `,
        /* highlight-start */
        setup: () => ({
          custom_namespaces: {
            itunes: 'http://www.itunes.com/dtds/podcast-1.0.dtd',
          },
          custom_elements: [
            { 'itunes:author': 'Michael Scott' },
            { 'itunes:explicit': 'clean' },
          ],
        }),
        /* highlight-end */
        feeds: [
          {
            ...
          },
        ],
      },
    },
  ],
}
```

## ¡Feliz blogueo!

Con el [Gatsby feed plugin](/packages/gatsby-plugin-feed/), puede compartir su escritura fácilmente con personas suscritas a través de lectores RSS como Feedly o RSS Feed Reader. Ahora que su feed está configurado, realmente no tendrá que pensar en ello; publique una nueva publicación, y su feed RSS se actualizará automáticamente con su compilación de Gatsby. ¡Voilà!

## Más recursos

[Jason Lengstorf y Amberley Romo en directo construyendo un sitio de podcast alimentado por RSS](https://www.youtube.com/watch?v=0hGlvyuQiKQ).
