---
title: "Tutorial del complemento WordPress Source"
---

## Cómo crear un sitio con datos extraídos de WordPress

### Qué cubre este tutorial:

En este tutorial, instalará el complemento `gatsby-source-wordpress` para extraer datos de blog e imágenes de una instalación de WordPress en su sitio de Gatsby y representar esos datos. Este [sitio de demostración de Gatsby + WordPress] (https://github.com/gatsbyjs/gatsby/tree/master/examples/using-wordpress) le muestra el código fuente de un sitio de ejemplo similar a lo que va a construir en este tutorial, aunque faltan las imágenes geniales que agregará en la siguiente parte de este tutorial, [Agregar imágenes a un sitio de WordPress] (/ tutorial / wordpress-image-tutorial /). :D

#### ¿Pero prefieres GraphQL?

Si prefiere usar GraphQL, hay un complemento [wp-graphql] (https://github.com/wp-graphql/wp-graphql) para exponer fácilmente los datos predeterminados y personalizados en WordPress.

Los mismos esquemas de autenticación admitidos por el WP-API se admiten en wp-graphql, que se puede usar con el complemento [gatsby-source-graphql] (/ packages / gatsby-source-graphql /).

## ¿Por qué pasar por este tutorial?

Si bien cada complemento de origen puede funcionar de manera diferente a los demás, vale la pena seguir este tutorial porque casi definitivamente usará un complemento de origen en la mayoría de los sitios de Gatsby que cree. Este tutorial lo guiará a través de los conceptos básicos para conectar su sitio Gatsby a un CMS, obtener datos y usar React para representar esos datos de manera hermosa en su sitio.

Si desea ver el creciente número de complementos de origen disponibles para usted, busque "origen" en la [biblioteca de complementos de Gatsby](/plugins/?=source).

### Crear un sitio con el complemento `gatsby-source-wordpress`

Cree un nuevo proyecto Gatsby y cambie los directorios al nuevo proyecto que acaba de crear:

```shell
 gatsby new wordpress-tutorial-site
cd wordpress-tutorial-site
```

Instala el complemento `gatsby-source-wordpress`. Para obtener más información sobre las características del complemento y ejemplos de consultas GraphQL no incluidas en este tutorial, consulte el [archivo README del complemento 'gatsby-source-wordpress`](/packages/gatsby-source-wordpress/?=wordpress).

```shell
npm install --save gatsby-source-wordpress
```

Agregue el complemento `gatsby-source-wordpress` a` gatsby-config.js` utilizando el siguiente código, que también puede encontrar en el [código fuente del sitio de demostración] (https://github.com/gatsbyjs/gatsby/blob/master/examples/using-wordpress/gatsby-config.js).

```js:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Gatsby WordPress Tutorial",
  },
  plugins: [
    // https://public-api.wordpress.com/wp/v2/sites/gatsbyjsexamplewordpress.wordpress.com/pages/
    /*
     * Gatsby's data processing layer begins with “source”
     * plugins. Here the site sources its data from WordPress.
     */
    // highlight-start
    {
      resolve: `gatsby-source-wordpress`,
      options: {
        /*
         * The base URL of the WordPress site without the trailingslash and the protocol. This is required.
         * Example : 'dev-gatbsyjswp.pantheonsite.io' or 'www.example-site.com'
         */
        baseUrl: `dev-gatbsyjswp.pantheonsite.io`,
        // The protocol. This can be http or https.
        protocol: `http`,
        // Indicates whether the site is hosted on wordpress.com.
        // If false, then the assumption is made that the site is self hosted.
        // If true, then the plugin will source its content on wordpress.com using the JSON REST API V2.
        // If your site is hosted on wordpress.org, then set this to false.
        hostingWPCOM: false,
        // If useACF is true, then the source plugin will try to import the WordPress ACF Plugin contents.
        // This feature is untested for sites hosted on WordPress.com
        useACF: true,
      },
    },
    // highlight-end
  ],
}
```

### Crear consultas GraphQL que extraen datos de WordPress

Ahora está listo para crear una consulta GraphQL para obtener algunos datos del sitio de WordPress. Creará una consulta que extraiga el título de las publicaciones del blog, la fecha en que se publicaron y el contenido de la publicación del blog.

Correr:

```shell
gatsby develop
```

In your browser, open localhost:8000 to see your site, and open localhost:8000/\_\_\_graphql so that you can create your GraphQL queries.

As an exercise, try re-creating the following queries in your GraphiQL explorer. This first query will pull in the blogpost content from WordPress:

```graphql
query {
  allWordpressPage {
    edges {
      node {
        id
        title
        excerpt
        slug
        date(formatString: "MMMM DD, YYYY")
      }
    }
  }
}
```

La siguiente consulta extraerá una lista ordenada de las publicaciones del blog:

```graphql
{
  allWordpressPost(sort: { fields: [date] }) {
    edges {
      node {
        title
        excerpt
        slug
      }
    }
  }
}
```

## Representar las publicaciones del blog en `index.js`

Ahora que ha creado las consultas de GraphQL que extraen los datos que desea, utilizará esa segunda consulta para crear una lista de títulos de publicaciones de blog ordenados en la página de inicio de su sitio. Así es como debería verse su `index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
import SEO from "../components/seo"

export default ({ data }) => {
  //highlight-line
  return (
    <Layout>
      <SEO title="home" />
      //highlight-start
      <h1>My WordPress Blog</h1>
      <h4>Posts</h4>
      {data.allWordpressPost.edges.map(({ node }) => (
        <div>
          <p>{node.title}</p>
          <div dangerouslySetInnerHTML={{ __html: node.excerpt }} />
        </div>
      ))}
      //highlight-end
    </Layout>
  )
}

//highlight-start
export const pageQuery = graphql`
  query {
    allWordpressPost(sort: { fields: [date] }) {
      edges {
        node {
          title
          excerpt
          slug
        }
      }
    }
  }
`
//highlight-end
```

Guarde estos cambios y revise localhost:8000 para ver su nueva página de inicio con una lista de publicaciones de blog ordenadas.

![Inicio de WordPress después de la consulta](/images/wordpress-source-plugin-home.jpg)

> ** NOTA: ** para futuros editores: sería útil tener también ejemplos de cómo cargar publicaciones de blog en sus propias páginas individuales. Y útil para insertar una captura de pantalla del resultado final aquí

## Cree páginas para cada publicación de blog y enlácelas

Una página de índice con un título y extracto de publicación es excelente, pero también debe crear páginas para cada una de las publicaciones del blog y vincularlas desde su archivo `index.js`.

Para hacer esto, necesitas:

1. Crear páginas para cada publicación de blog
2. Enlace el título en la página de índice con la página de publicación.

Si aún no lo ha hecho, lea la [Parte 7] (/tutorial/part-seven/) del tutorial fundamental, ya que trata el concepto y los ejemplos de este proceso con Markdown en lugar de WordPress.

### Crear páginas para cada publicación de blog.

En la Parte 7 del tutorial, el primer paso para crear páginas es crear slugs para los archivos de markdown. Como está utilizando WordPress y no archivos de Markdown, puede tomar las babosas que se devuelven de su llamada API a la fuente de WordPress. Puede omitir la creación de babosas, ya que ya las tiene.

Abra su archivo `gatsby-node.js` en la raíz de su proyecto (debe estar en blanco excepto por algunos comentarios) y agregue lo siguiente:

```js:title=gatsby-node.js
const path = require(`path`)

exports.createPages = ({ graphql, actions }) => {
  const { createPage } = actions
  return graphql(`
    {
      allWordpressPost(sort: { fields: [date] }) {
        edges {
          node {
            title
            excerpt
            content
            slug
          }
        }
      }
    }
  `).then(result => {
    console.log(JSON.stringify(result, null, 4))
  })
}
```

A continuación, detenga y reinicie el entorno `gatsby develop`. Mientras observa el terminal, debería ver dos objetos Post registrados en el terminal:

![Two posts logged to the terminal](/images/wordpress-source-plugin-log.jpg)

¡Excelente! Como se explica en la Parte 7 del tutorial, esta exportación `createPages` es uno de los "caballos de batalla" de Gatsby y nos permite crear sus publicaciones de blog (o páginas, o tipos de publicaciones personalizadas, etc.) desde su instalación de WordPress.

Sin embargo, antes de poder crear las publicaciones de blog, debe especificar una plantilla para crear las páginas.

En su directorio `src`, cree un directorio llamado `templates` y en la carpeta `templates` recién creada, cree un archivo llamado `blog-post.js`. En ese nuevo archivo, pegue lo siguiente:

```jsx:title=src/tempates/blog-post.js
import React from "react"
import Layout from "../components/layout"
import { graphql } from "gatsby"

export default ({ data }) => {
  const post = data.allWordpressPost.edges[0].node
  console.log(post)
  return (
    <Layout>
      <div>
        <h1>{post.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.content }} />
      </div>
    </Layout>
  )
}
export const query = graphql`
  query($slug: String!) {
    allWordpressPost(filter: { slug: { eq: $slug } }) {
      edges {
        node {
          title
          content
        }
      }
    }
  }
`
```

¿Qué está haciendo este archivo? Después de importar sus dependencias, construye el diseño de la publicación con JSX. Envuelve todo en el componente `Layout`, por lo que el estilo es el mismo en todo el sitio. Luego, simplemente agrega el título de la publicación y el contenido de la publicación. Puede agregar cualquier cosa que desee y puede consultar aquí (por ejemplo, imagen característica, meta de publicación, campos personalizados, etc.).

Debajo de eso, puede ver la consulta GraphQL llamando a la publicación específica basada en el `$slug`. Esta variable se pasa a la plantilla `blog-post.js` cuando la página se crea en `gatsby-node.js`. Para lograr esto, agregue el siguiente código al archivo `gatsby-node.js`:

```js:title=gatsby-node.js
const path = require(`path`)

exports.createPages = ({ graphql, actions }) => {
  const { createPage } = actions
  return graphql(`
    {
      allWordpressPost(sort: { fields: [date] }) {
        edges {
          node {
            title
            excerpt
            content
            slug
          }
        }
      }
    }
  `).then(result => {
    //highlight-start
    result.data.allWordpressPost.edges.forEach(({ node }) => {
      createPage({
        path: node.slug,
        component: path.resolve(`./src/templates/blog-post.js`),
        context: {
          // This is the $slug variable
          // passed to blog-post.js
          slug: node.slug,
        },
      })
    })
    //highlight-end
  })
}
```

Deberá detenerse y volver a iniciar su entorno utilizando `gatsby develop`. Cuando lo haga, no verá un cambio en la página de índice del sitio, pero si navega a una página 404, como [http://localhost:8000/asdf] (http://localhost:8001/asdf) , debería ver las dos publicaciones de muestra creadas y poder hacer clic en ellas para ir a las publicaciones de muestra:

![Ejemplos de enlaces de publicaciones](/images/wordpress-source-plugin-sample-post-links.gif)

¡Pero a nadie le gusta ir a una página 404 para encontrar una publicación de blog! Entonces, vinculemos esto desde la página de inicio.

### Vinculación a publicaciones de la página de inicio.

Dado que ya tiene su estructura y consulta para la página `index.js`, todo lo que necesita hacer es usar el componente` Link` para ajustar sus títulos y debería estar listo.

Open up your `index.js` file and add the following:

```jsx:title=src/pages/index.js
import React from "react"
import { Link, graphql } from "gatsby" //highlight-line
import Layout from "../components/layout"
import SEO from "../components/seo"

export default ({ data }) => {
  return (
    <Layout>
      <SEO title="home" />
      <h1>My WordPress Blog</h1>
      <h4>Posts</h4>
      {data.allWordpressPost.edges.map(({ node }) => (
        <div>
          //highlight-start
          <Link to={node.slug}>
            <p>{node.title}</p>
          </Link>
          //highlight-end
          <div dangerouslySetInnerHTML={{ __html: node.excerpt }} />
        </div>
      ))}
    </Layout>
  )
}

export const pageQuery = graphql`
  query {
    allWordpressPost(sort: { fields: [date] }) {
      edges {
        node {
          title
          excerpt
          slug
        }
      }
    }
  }
`
```

¡Y eso es! Cuando envuelva el título en el componente `Link` y haga referencia a la publicación de la publicación, Gatsby agregará algo de magia al enlace, lo precargará y hará que la transición entre páginas sea increíblemente rápida:

![Producto final con enlaces desde la página de inicio a las publicaciones del blog](/images/wordpress-source-plugin-home-to-post-links.gif)

### Resumiendo.

Puede aplicar el mismo procedimiento para llamar y crear páginas, tipos de publicaciones personalizadas, campos personalizados, taxonomías y todo el contenido divertido y flexible por el que WordPress es conocido. Esto puede ser tan simple o complejo como te gustaría que fuera, ¡así que explora y diviértete!