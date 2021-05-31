---
title: Uso de Prismic con el Plugin de Fuente de GraphQL
---

## Características de Prismic + Gatsby

Prismic es un sistema de gestión de contenidos o CMS _headless_, el mismo que provee una aplicación web que permite a los creadores de contenido enforcarse en crear y modificar el contenido de su sitio. En esencia, se distingue gracias a su experiencia de usuario (UX) que permite bastante flexibilidad sin complicaciones. Aquí la característica de _Slices_ juega un papel muy importante, ya que estos corresponden a componentes en la aplicación web que gente 'no técnica' puede usar para montar su página.
Usado en conjunto con Gatsby, te permite crear sitios rápidos y editables.

Nota que el plugin de fuente de Gatsby Prismic que usarás durante este tutorial, tiene, como su característica principal, **vistas previas reales** de tus páginas para que puedas saber cómo se verán antes de publicarlas o desarrollarlas. Además, puedes generar **enlaces para compartir** que pueden ser vistos incluso por quienes no son usuarios de Prismic.

## ¿Qué contiene este tutorial?

Al terminar este tutorial, habrás hecho lo siguiente:

- Aprendido cómo configurar la última versión del plugin de fuente de Prismic
- Extraer y renderizar datos desde un repositorio de Prismic
- Crear páginas mediante programación desde una fuente de Prismic
- Configurar vistas previas para documentos editados y no publicados

## Prerrequisitos

- Debes estar familiarizado con Gatsby
- Un repositorio personal en Prismic. Puedes seguir [esta guía de 5 minutos](https://prismic.io/docs/reactjs/getting-started/create-repo-minimalist-blog) con instrucciones para configurar un repositorio básico para un blog minimalista.

## Preparación de tu ambiente

Empieza un nuevo proyecto en Gatsby usando el _starter_ por defecto.

    $ gatsby new gatsby-prismic-blog
    $ cd gatsby-prismic-blog

Ahora, tendrás que instalar los paquetes faltantes. Este comando incluye el plugin de fuente de Gatsby Prismic, y los kits de Prismic para facilitar procesos en React:

    $ npm i --save gatsby-source-prismic-graphql prismic-javascript prismic-reactjs

Si quieres enfocarte sólo en aprender como extraer y renderizar datos desde un repositorio Prismic, puedes usar el repositorio de ejemplo `gatsby-blog-scratch` pero debes crear el tuyo para que puedas modificar el contenido y probar las vistas previas. De lo contrario, puedes seguir [este artículo](https://prismic.io/docs/reactjs/getting-started/create-repo-minimalist-blog) para crear tu propio repositorio Prismic. Se recomienda escribir algunos posts en el blog para que tengas contenido que mostrar.

## Configuración del plugin

Configurarás el plugin de fuente de Gatsby para que pueda extraer datos desde el repositorio Prismic. Para esto, la única opción que debes especificar es el nombre del repositorio.

```javascript:title=gatsby-config.js
{
  resolve: `gatsby-source-prismic-graphql`,
  options: {
    repositoryName: 'gatsby-blog-scratch'
  }
},
```

Si ejecutas `gatsby develop` ahora, deberías tener acceso a los datos de Prismic a través de la interfaz de GraphiQL en `http://localhost:8000/___graphql`. Puedes verificar que funcione intentando hacer una consulta que usa como fuente a Prismic.

```graphql
{
  prismic {
    _allDocuments {
      edges {
        node {
          __typename
        }
      }
    }
  }
}
```

¡Si puedes obtener tus documentos de Prismic, entonces sabremos que la configuración fue exitosa!

## Extracción y renderización de datos

Una vez que hayas verificado en GraphiQL que es posible obtener datos desde tu repositorio Prismic creado anteriormente, podrás empezar a extraer y renderizar ese contenido.

Experimenta con los datos y su estructura en GraphiQL. Puedes usar el autocompletado como ayuda para entender cómo Gatsby interpreta el repositorio de Prismic. Necesitarás una consulta que obtenga la información de Home, así como un arreglo de los posts del blog ordenados descendentemente.

```jsx:title=src/pages/index.js
import React from "react"
import { Link, graphql } from "gatsby" //highlight-line

import Layout from "../components/layout"
import { RichText } from "prismic-reactjs" //highlight-line

//highlight-start
export const query = graphql`
  {
    prismic {
      allBlog_homes {
        edges {
          node {
            headline
            description
            image
          }
        }
      }
      allPosts(sortBy: date_DESC) {
        edges {
          node {
            _meta {
              id
              uid
              type
            }
            title
            date
          }
        }
      }
    }
  }
`
// highlight-end
```

Para renderizar estos datos, reemplaza la línea `export default IndexPage` en el archivo original `index.js` con lo siguiente:

```jsx:title=src/pages/index.js
export default ({ data }) => {
  const doc = data.prismic.allBlog_homes.edges.slice(0, 1).pop()
  const posts = data.prismic.allPosts.edges

  if (!doc) return null

  return (
    <Layout>
      <div>
        <img src={doc.node.image.url} alt={doc.node.image.alt} /> // Asegúrate
          de añadir el atributo de accesibilidad cuando agregues imágenes en
          Prismic: https://user-guides.prismic.io/articles/768849-add-metadata-to-an-asset
        <h1>{RichText.asText(doc.node.headline)}</h1>
        <p>{RichText.asText(doc.node.description)}</p>
      </div>
    </Layout>
  )
}
```

Guarda el archivo y verifica que tu sitio está siendo ejecutado en `http://localhost:8000`

Puedes usar la función auxiliar `RichText` para [renderizar texto con formato](https://prismic.io/docs/reactjs/rendering/rich-text), generalmente, este será el proceso que usarás para consultar y renderizar tu repositorio Prismic. Podemos limpiar esto un poco más e incluir una función que renderice el arreglo de los posts del blogs que consultamos previamente.

```jsx:title=src/pages/index.js
//highlight-start
const BlogPosts = ({ posts }) => {
  if (!posts) return null
  return (
    <div>
      {posts.map(post => {
        return (
          <div key={post.node._meta.id}>
            <h2>{RichText.asText(post.node.title)}</h2>
            <p>
              <time>{post.node.date}</time>
            </p>
          </div>
        )
      })}
    </div>
  )
}
//highlight-end

export default ({ data }) => {
  const doc = data.prismic.allBlog_homes.edges.slice(0, 1).pop()
  const posts = data.prismic.allPosts.edges

  if (!doc) return null

  return (
    <Layout>
      <div>
        <img src={doc.node.image.url} alt={doc.node.image.alt} />
        <h1>{RichText.asText(doc.node.headline)}</h1>
        <p>{RichText.asText(doc.node.description)}</p>
      </div>
      <BlogPosts posts={posts} /> //highlight-line
    </Layout>
  )
}
```

## Construcción de enlaces a tus documentos

Ahora las cosas van tomando forma. Transformaremos los títulos de los posts del blog en enlaces, creando una [función gestora de enlaces (Link Resolver)](https://prismic.io/docs/reactjs/beyond-the-api/link-resolving), la cual construirá la ruta correcta para tus posts del blog.

```javascript:title=src/utils/linkResolver.js
exports.linkResolver = function linkResolver(doc) {
  // Rutas para los posts del blog
  if (doc.type === "post") {
    return "/blog/" + doc.uid
  }
  // Ruta alternativa a la página de inicio
  return "/"
}
```

El objetivo de esta función es generar una url de navegación que dependa del tipo de documento. En este caso será `/blog/{slug único}` para documentos del tipo `post` y la carpeta raíz `/` para cualquier otro tipo de documento, incluyendo `blog_home`. Como puedes ver, para generar una url adecuada con esta función auxiliar, los datos requeridos son: el tipo de documento y un identificador único. Estos campos están siempre presentes como parte del campo `_meta`, así que asegúrate de obtenerlo en tu consulta.

Tendrás que configurar tu archivo `gatsby-browser.js` para que también use el Gestor de Enlaces.

```javascript:title=gatsby-browser.js
const { registerLinkResolver } = require("gatsby-source-prismic-graphql")
const { linkResolver } = require("./src/utils/linkResolver")

registerLinkResolver(linkResolver)
```

Ahora puedes usar la url adecuada generada por la función `linkResolver` para crear el componente `<Link>` para cada post del blog, de esta manera, ahora los títulos de los posts serán links.

```jsx:title=src/pages/index.js
const BlogPosts = ({ posts }) => {
  if (!posts) return null
  return (
    <ul>
      {posts.map(post => {
        return (
          <li key={post.node._meta.id}>
            // highlight-start
            <Link to={linkResolver(post.node._meta)}>
              {RichText.asText(post.node.title)}
            </Link>
            // highlight-end
            <p>
              <time>{post.node.date}</time>
            </p>
          </li>
        )
      })}
    </ul>
  )
}
```

En este punto, si intentas usar estos enlaces para navegar por tu sitio, encontrarás errores 404 en cada página. Esto sucede porque, aunque estás navegando por las páginas correctamente, aún existe el problema de que las páginas no se están creando de manera adecuada. Para esto, deberás usar un archivo plantilla el cual creará, por medio de programación, una página por cada post del blog.

## Creación de páginas mediante programación con una plantilla

La plantilla que desarrollarás es muy similiar, en concepto, a una página regular, con la diferencia de que esta introduce una variable que será usada para consultar los diferentes posts del blog.

```jsx:title=/src/templates/post.js
import React from "react"
import { graphql, Link } from "gatsby"
import { RichText } from "prismic-reactjs"

export const query = graphql`
  query BlogPostQuery($uid: String) {
    prismic {
      allPosts(uid: $uid) {
        edges {
          node {
            title
            date
            post_body
          }
        }
      }
    }
  }
`

export default ({ data }) => {
  const doc = data.prismic.allPosts.edges.slice(0, 1).pop()
  if (!doc) return null

  return (
    <div>
      <Link to="/">
        <span>go back</span>
      </Link>
      <h1>{RichText.asText(doc.node.title)}</h1>
      <span>
        <em>{doc.node.date}</em>
      </span>
      <div>{RichText.render(doc.node.post_body)}</div>
    </div>
  )
}
```

Estamos renderizando una página bastante minimalista para cada post del blog, que consiste de:

- Un link para regresar a la página de inicio.
- El título del artículo y página.
- El texto enriquecido del cuerpo del post que contendrá texto formateado e imágenes.

Tener una plantilla no es suficiente para generar páginas dinámicas, además deberás configurar el plugin en `gatsby-config.js` para que las páginas sean creadas siguiendo el mismo patrón definido en la función de gestión de enlaces (Link Resolver).

```javascript:title="/gatsby-config.js"
options: {
  repositoryName: 'gatsby-blog-scratch',
  //highlight-start
  pages: [{
    type: 'Post',          // Tipo personalizado del documento
    match: '/blog/:uid',   // Las páginas serán generadas con este patrón
    path: '/blog-preview', // Ruta para vista previa
    component: require.resolve('./src/templates/post.js') // Archivo plantilla
  }]
  //highlight-end
}
```

Y con este paso final deberías ver todos tus posts del blog renderizados en tu sitio.

## Configuración de vistas previas

Una de las características más emocionantes que este plugin de fuente de Gatsby Prismic provee, es la habilidad de previsualizar cambios de tus documentos sin tener que publicarlos o recompilar tu aplicación de Gatsby. Para activar esto, primero tienes que configurar un _endpoint_ en tu repositorio Prismic.

En tu repositorio, ve a **Settings > Previews > Create a New Preview** y llena los campos referentes a tu proyecto. Para un ambiente de desarrollo local debes usar `http://localhost:8000` como el Dominio, con `/preview` como el Gestor de Enlaces opcional. No te preocupes en incluir el script del toolbar, el plugin se encargará de eso.

Finalmente, regresa a tu archivo de configuración de Gatsby para activar la característica.

```javascript:title="/gatsby-config.js"

{
  resolve: `gatsby-source-prismic-graphql`,
  options: {
    repositoryName: 'gatsby-blog-scratch',
    //highlight-start
    previews: true,
    path: '/preview',
    //highlight-end
    pages: [{
      type: 'Post',
      match: '/blog/:uid',
      path: '/blog-preview',
      component: require.resolve('./src/templates/post.js')
    }]
  }
}
```

Ahora tu blog está listo para manejar vistas previas. Solamente edita cualquiera de tus posts del blog en tu repositorio Prismic y previsualiza los cambios que haces en vez de publicarlos. Las vistas previas no están limitadas al ambiente de desarrollo, puedes ajustar la configuración del _endpoint_ para que funcione con la versión alojada que despliegues. Creadores de contenido pueden usar esto como un ambiente de pre-producción para visualizar sus cambios de contenido antes de publicarlos y sin tener que recompilar el sitio.

## ¿Qué acabas de construir?

Luego de seguir este tutorial tienes un blog minimalista que usa un repositorio Prismic como fuente de datos. Has aprendido:

- Cómo consultar datos relevantes con GraphQL.
- Renderizar datos en tu sitio.
- Crear plantillas para generar páginas mediante programación.
- Construir enlaces para navegar en el sitio.
- Y más importante, cómo configurar vistas previas para que puedas ver los cambios de tus documentos sin publicarlos.

## ¿A dónde ir desde aquí?

Si quieres ir más lejos, aquí hay algunos temas avanzados que puedes hacer usando Prismic:

- Renderización de [componentes _slice_](https://www.youtube.com/watch?v=N85Tw06e29Q) para construir páginas modulares.
- Uso de [webhooks](https://user-guides.prismic.io/webhooks/webhooks) como un disparador para recompilar tu sitio.
- Uso de una [función auxiliar](https://prismic.io/docs/reactjs/getting-started/prismic-gatsby#27_0-using-the-html-serializer) para cambiar los enlaces que están adentro de campos de texto enriquecido para enlazar componentes.

Puedes leer más sobre esto en [documentacación de Gatsby en Prismic](https://prismic.io/docs/reactjs/getting-started/prismic-gatsby), haz tu [blog con todas las funcionalidades](https://user-guides.prismic.io/examples/gatsby-js-samples/sample-blog-with-api-based-cms-gatsbyjs) donde puedes probar los _Slices_.
