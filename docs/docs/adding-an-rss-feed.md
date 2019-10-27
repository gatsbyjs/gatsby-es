---
title: Agregando un Feed RSS
---

## ¿Qué es un feed RSS?

Un [feed RSS](https://en.wikipedia.org/wiki/RSS) es un archivo estándar XML que enumera el contenido del sitio en un formato suscribible, que permite a los lectores consumir su contenido en agregadores de noticias, también conocidos como aplicaciones de lector de feeds.

Piensa en ello como un canal de distribución asociado para el contenido de tu sitio.

## Instalación

Para generar un feed RSS, puedes usar el paquete [`gatsby-plugin-feed`](/packages/gatsby-plugin-feed/). Para instalar este paquete, ejecuta el siguiente comando:

```shell
npm install --save gatsby-plugin-feed
```

## Como usar [gatsby-plugin-feed](/packages/gatsby-plugin-feed/)

Cuando la instalación esté completa, podrás agregar este paquete al archivo de configuración de tu sitio, de la siguiente manera:

```js:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    siteUrl: `https://www.example.com`,
  },
  plugins: [`gatsby-plugin-feed`],
}
```

Aquí hay un ejemplo de como implementar este complemento con Markdown, pero para otras fuentes, necesitarás una forma de identificar de forma exclusiva el contenido, generalmente con la URL o con un slug.

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

Posteriormente, ejecute una compilación (`npm run build`) ya que la generación de feeds RSS solamente se realizará para las compilaciones de producción. Por defecto, la ruta donde se generan los feeds RSS es `/rss.xml`, pero el complemento expone opciones para configurar esta funcionalidad predeterminada.

Para configuraciones básicas con contenido Markdown como [gatsby-starter-blog](https://github.com/gatsbyjs/gatsby-starter-blog), ¡eso es todo lo que necesitas! Sin embargo, puedes crear un esquema de feeds RSS personalizado, modificando los archivos `gatsby-node.js` y `gatsby-config.js`.

## Personalización del complemento de feed RSS

Tu contenido podría no encajar perfectamente en el escenario de inicio de blog, por varias razones como:

- Tu contenido no está en Markdown, por lo que el complemento no lo identifica
- Tus archivos Markdown tienen fechas en los nombres de archivo, por lo que las URL de slug provocan un error 404

La buena noticia es que puedes acomodar estos escenarios y más en `gatsby-config.js` y `gatsby-node.js`.

Para configurar el esquema por defecto (también conocido como estructura) que genera el complemento para que funcione con el contenido de tu sitio web, puedes comenzar con el siguiente código:

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

Este fragmento de código contiene una configuración personalizada de `gatsby-plugin-feed` en `gatsby-config.js` para consultar los metadatos de tu sitio, como tu `title` y `siteUrl`. Tambien incluye una matriz de `feeds` con al menos un objeto que contiene una consulta GraphQL y un método `serialize`, que permite generar una estructura de feeds RSS personalizada. En este ejemplo, el contenido RSS proviene de archivos Markdown provenientes de su sitio, y se consultan con la llave `allMarkdownRemark` y sus filtros y campos asociados.

El campo `output` de su objeto te permite personalizar el nombre del archivo para tu feed RSS y el `title` para el nombre del feed RSS de tu sitio.

Por defecto, se hace referencia al feed en todas las páginas. Puedes personalizar este comportamiento proporcionando un campo adicional `match` de tipo `string`. Esta cadena se usará para construir una `RegExp`, y esta expresión regular se usará para probar el `pathname` de la página actual. Solo las páginas que satisfacen la explesión regular tendrán referencia del feed incluido.

Para ver tu feed en acción, ejecuta `gatsby build && gatsby serve` y luego inspecciona el contenido y las URL's de tu archivo RSS en `http://localhost:9000/rss.xml`.

> NOTA: si tu blog tiene enlaces permanentes personalizados, como enlaces con o sin fechas en ellos, es posible que deba [modificar `gatsby-node.js`](https://github.com/gatsbyjs/gatsby-starter-blog/blob/master/gatsby-node.js#L57) para generar URL's correctas en tus feeds RSS. ¡[Ponte en contacto con nosotros](/contributing/how-to-contribute/) si necesitas ayuda!

## Sintaxis para bloques RSS de iTunes

Si crea una fuente RSS para un podcast, es probable que desee incluir bloques RSS de iTunes. Toman el formato de `itunes: author` que GraphQL no lee. Aquí hay un ejemplo de cómo implementar bloques RSS de iTunes usando este complemento:

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

Con el [complemento Gatsby feed](/packages/gatsby-plugin-feed/), podrás compartir lo que escribes fácilmente con las personas suscritas a través de lectores RSS como Feedly o RSS Feed Reader. Ahora que tu feed está configurado, realmente no tendrás que pensarlo; realiza una nueva publicación, y tu feed RSS se actualizará automáticamente con tu compilación de Gatsby. Voilà!

## Más recursos

[Jason Lengstorf and Amberley Romo livestream building an RSS feed powered podcast site](https://www.youtube.com/watch?v=0hGlvyuQiKQ).
