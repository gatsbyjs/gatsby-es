---
title: Obteniendo datos desde Sanity
---

## ¿Qué es Sanity.io?

[Sanity](https:///www.sanity.io) es un backend alojado para contenido estructurado que viene con un editor de código libre creado con React. Tiene potentes APIs en tiempo real tanto para leer como escribir datos.

Puedes usar Sanity como un _headless CMS_ que permite a tus autores trabajar en un entorno amigable, o como un backend puro para tus aplicaciones. Te hacemos más fácil la reutilización de contenido en varios sitios web, aplicaciones, impresión, asistentes de voz, y otros canales.

## Empezando

Comienza configurando un proyecto en Gatsby. Si quieres empezar desde cero, la [Guía de Inicio Rápido](/docs/quick-start) es un buen lugar para empezar. Vuelva a esta guía cuando lo tengas configurado.

También puedes consultar [el ejemplo en el sitio web de la compañía](https://github.com/sanity-io/example-company-website-gatsby-sanity-combo) que hemos configurado. Contiene configurados ambos _Sanity Studio_ y un _frontend_ con Gatsby, que puedes poner en marcha en cuestión de minutos. Puede ser una referencia útil sobre cómo construir un sitio web usando contenido estructurado. Sigue las instrucciones del archivo README.md para empezar a funcionar.

Esta guía cubre cómo configurar y usar el plugin [`gatsby-source-sanity`](https://www.npmjs.com/package/gatsby-source-sanity).

## Uso básico

```shell
npm install --save gatsby-source-sanity
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-source-sanity",
      options: {
        projectId: "abc123",
        dataset: "blog",
      },
    },
  ],
}
```

En este punto puedes elegir (y probablemente deberías) [configurar una API de GraphQL](https://www.sanity.io/help/graphql-beta) para tu conjunto de datos de Sanity, si aún no lo has hecho. Esto ayudará al plugin conocer qué tipo de datos y campos existen, para que puedas consultarlos incluso sin que estén presentes en ningún documento actual.

Ves a `http://localhost:8000/___graphql` después de ejecutar `gatsby develop` para entender los datos creados. Crea una nueva consulta y verifica las colecciones y campos disponibles usando el autocompletado (`CTRL + ESPACIO`).

## Opciones

| Opciones       | Tipo    | Por Defecto | Descripción                                                                                                                                        |
| -------------- | ------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| projectId      | string  |             | **[requerido]** El ID de tu proyecto en Sanity                                                                                                     |
| dataset        | string  |             | **[requerido]** El conjunto de datos a obtener                                                                                                     |
| token          | string  |             | Token de autenticación para obtener conjuntos de datos privados, o cuando uses `overlayDrafts` [Aprende más](https://www.sanity.io/docs/http-auth) |
| overlayDrafts  | boolean | `false`     | Establecer en `true` para que los borradores reemplacen su versión publicada. Por defecto, los borradores se omitirán.                             |
| watchMode      | boolean | `false`     | Establecer en `true` para mantener un _listener_ abierto y actualizar con los últimos cambios en tiempo real.                                      |

## Campos faltantes

¿Obteniendo errores como estos?

> Cannot query field "allSanityBlogPost"
> Unknown field `preamble` on type `BlogPost`

Al [implementar una API GraphQL](https://www.sanity.io/help/graphql-beta) para tu conjunto de datos, podemos inspeccionar y descubrir qué esquemas y campos están disponibles y ponerlos a disposición para evitar este problema. Una vez que implementes la API se aplicará de forma transparente. Si has implementado tu API y aún ves problemas similares, recuerda que debes volver a implementar la API si tu esquema cambia.

Algunos antecedentes para este problema:

Gatsby no puede conocer sobre los tipos y campos sin tener documentos de los tipos dados que contienen los campos que quieres consultar. Esto es un [problema conocido](https://github.com/gatsbyjs/gatsby/issues/3344) con Gatsby - afortunadamente hay trabajo en marcha para resolver este problema, que conducirá a esquemas más claros y menos _plantillas_.

## Usando imágenes

Los campos de imagen tendrán la URL de la imagen disponible bajo la clave `field.asset.url`, pero también puedes usar [gatsby-image](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-image) para una experiencia fluida. Es un componente React que habilita imágenes adaptables y técnicas avanzadas de carga de imágenes. Funciona muy bien con este plugin, sin requerir pasos adicionales en el _build_.

Hay dos tipos de imágenes adaptables soportadas; _fixed_ y _fluid_. Para decidir entre las dos, pregúntate: "¿sé el tamaño exacto que tendrá esta imagen?" En caso afirmativo, querrás usar _fixed_. En caso contrario y su ancho y/o altura necesitan variar dependiendo del tamaño de la pantalla, entonces querrás usar _fluid_.

### _Fluid_

```jsx
import React from "react"
import Img from "gatsby-image"

const Person = ({ data }) => (
  <article>
    <h2>{data.sanityPerson.name}</h2>
    <Img fluid={data.sanityPerson.profileImage.asset.fluid} />
  </article>
)

export default Person

export const query = graphql`
  query PersonQuery {
    sanityPerson {
      name
      profileImage {
        asset {
          fluid(maxWidth: 700) {
            ...GatsbySanityImageFluid
          }
        }
      }
    }
  }
`
```

### _Fixed_

```jsx
import React from "react"
import Img from "gatsby-image"

const Person = ({ data }) => (
  <article>
    <h2>{data.sanityPerson.name}</h2>
    <Img fixed={data.sanityPerson.profileImage.asset.fixed} />
  </article>
)

export default Person

export const query = graphql`
  query PersonQuery {
    sanityPerson {
      name
      profileImage {
        asset {
          fixed(width: 400) {
            ...GatsbySanityImageFixed
          }
        }
      }
    }
  }
`
```

### Fragmentos disponibles

Estos son los fragmentos disponibles en los archivos de imagen, que permiten buscar fácilmente los campos requeridos por _gatsby-image_ en varios modos:

- `GatsbySanityImageFixed`
- `GatsbySanityImageFixed_noBase64`
- `GatsbySanityImageFixed_withWebp`
- `GatsbySanityImageFixed_withWebp_noBase64`
- `GatsbySanityImageFluid`
- `GatsbySanityImageFluid_noBase64`
- `GatsbySanityImageFluid_withWebp`
- `GatsbySanityImageFluid_withWebp_noBase64`

## Borradores superpuestos _overlayDrafts_

A veces puedes estar trabajando en un contenido nuevo que aún no está publicado, del cual quieres asegurarte que se ve bien en tu sitio Gatsby. Al establecer el parámetro `overlayDrafts` en `true`, las versiones en borrador, como la opción dice, se superpondrán al documento actual. En términos de nodos de Gatsby, _reemplazará_ el documento publicado con el borrador.

Ten en cuenta que los borradores no tienen que ajustarse a ninguna regla de validación, por lo que en tu _frontend_ generalmente querrás verificar dos veces todas las propiedades anidadas antes de intentar usarlas.

## Modo _watchMode_

Durante el desarrollo, a veces puede ser beneficioso obtener actualizaciones sin tener que reiniciar manualmente el proceso del _build_. Al establecer `watchMode` en `true`, este plugin configurará un _listener_ que se mantiene atento a cambios. Cuando detecta un cambio, el documento en cuestión es actualizado en tiempo real y se reflejará inmediatamente.

Si añades un [token de entorno](#using-env-variables) y estableces `overlayDrafts` en `true`, cada pequeño cambio en el borrador será aplicado inmediatamente.

## Generando páginas

Sanity no tiene ningún concepto de "página", ya que está diseñado para ser totalmente independiente de cómo deseas presentar tu contenido y en qué medio, pero ya que estás usando Gatsby, ¡querrás probablemente algunas páginas!

Como en cualquier sitio Gatsby, tendrás que crear un archivo `gatsby-node.js` en la raíz del repositorio de tu sitio Gatsby (si aún no existe), y declarar una función `createPages`. Dentro de ella, usarás GraphQL para consultar los datos que necesitas para crear las páginas.

Por ejemplo, si tienes un tipo de documento `project` en Sanity del que quieres crear páginas, puedes hacer algo parecido a las siguientes líneas:

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  const result = await graphql(`
    {
      allSanityProject(filter: { slug: { current: { ne: null } } }) {
        edges {
          node {
            title
            description
            tags
            launchDate(format: "DD.MM.YYYY")
            slug {
              current
            }
            image {
              asset {
                url
              }
            }
          }
        }
      }
    }
  `)

  if (result.errors) {
    throw result.errors
  }

  const projects = result.data.allSanityProject.edges || []
  projects.forEach((edge, index) => {
    const path = `/project/${edge.node.slug.current}`

    createPage({
      path,
      component: require.resolve("./src/templates/project.js"),
      context: { slug: edge.node.slug.current },
    })
  })
}
```

La consulta anterior buscará todos los proyectos que tienen un campo `slug.current`, y generará páginas para ellos, disponibles como `/project/<project-slug>`. Usará el _template_ definido en `src/templates/project.js` como base para estas páginas.

Muchos [_starters_ de Gatsby](/starters/?v=2) tienen algún ejemplo de creación de páginas, que deberías poder modificar según tus necesidades.

Recuerda usar la interfaz GraphiQL para ayudarte a escribir las consultas que necesitas - generalmente se ejecuta en `http://localhost:8000/___graphql` mientras usas `gatsby develop`.

## Campos _"Raw"_

_Arrays_ y tipos de objetos en la raíz de los documentos obtendrán una representación adicional _"raw JSON"_ en un campo llamado  `_raw<FieldName>`. Por ejemplo, un campo llamado `body` será asignado a `_rawBody`. Es importante tener en cuenta que esto solo se hace con nodos de nivel superior (documentos).

## Texo Portable / Contenido de Bloque

El texto enriquecido en Sanity se representa normalmente como [Texto Portable](https://www.portabletext.org/) (anteriormente conocido como "Contenido de Bloque").

Estas estructuras de datos pueden ser profundas y una tarea difícil de consultar (especificando todos los campos posibles). Como [se indica arriba](#raw-fields), hay una alternativa _"raw"_ disponible para estos campos que es lo que normalmente querrás usar.

Puedes instalar [block-content-to-react](https://www.npmjs.com/package/@sanity/block-content-to-react) desde _npm_ y usarlo en tu proyecto Gatsby para serializar Texto Portable. Te deja usar tus propios componentes React para sobrescribir los predeterminados y renderizar tipos de contenido personalizados. [Aprende más sobre Texto Portable en nuestra documentación](https://www.sanity.io/docs/content-studio/what-you-need-to-know-about-block-text).

## Usando variables .env

Si no quieres añadir el ID de tu proyecto Sanity en el repositorio, puedes guardarlo fácilmente en archivos .env haciendo lo siguiente:

```js
// En tu archivo .env
SANITY_PROJECT_ID = abc123
SANITY_DATASET = production
SANITY_TOKEN = mi-token-super-secreto

// En tu archivo gatsby-config.js
require('dotenv').config({
  path: `.env.${process.env.NODE_ENV}`
})

module.exports = {
  plugins: [
    {
      resolve: 'gatsby-source-sanity',
      options: {
        projectId: process.env.SANITY_PROJECT_ID,
        dataset: process.env.SANITY_DATASET
        token: process.env.SANITY_TOKEN
      }
    }
  ]
}
```

Este ejemplo se basa en [la implementación de la Documentación de Gatsby](/docs/environment-variables/).
