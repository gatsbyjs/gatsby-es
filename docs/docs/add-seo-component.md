---
title: "Agregar un componente de SEO"
---

Cada sitio en la web tiene _meta-tags_ básicos como el título, favicon o descripción de la página en su elemento `<head>`. Esta información se muestra en el navegador y se usa cuando alguien comparte tu sitio web, por ejemplo en Twitter. Puedes proporcionar a tus usuarios y a estos sitios web datos adicionales para integrar tu sitio web con más datos — y aquí es donde entra esta guía para un componente de SEO. Al final tendrás un componente que podrás colocar en tu archivo _layout_ y tener previsualizaciones enriquecidas para otros clientes, usuarios de teléfonos inteligentes, y buscadores.

_Nota: Este componente usará StaticQuery. Si no estás familiarizado con esto, echa un vistazo a la [documentación de StaticQuery](/docs/static-query/). También debes tener `react-helmet` instalado, para lo cual puedes echar un vistazo a [este documento](/docs/add-page-metadata)._

## gatsby-config.js

Gatsby pone todos los datos de la sección `siteMetadata` de tu archivo `gatsby-config` disponibles de forma automática en GraphQL y, por lo tanto, es una buena idea colocar tu información para el componente allí.

```js:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Severus Snape",
    titleTemplate: "%s · The Real Hero",
    description:
      "Hogwarts Potions master, Head of Slytherin house and former Death Eater.",
    url: "https://www.doe.com", // ¡No se permite la barra inclinada final!
    image: "/images/snape.jpg", // Ruta a la imagen que colocaste en la carpeta 'static'
    twitterUsername: "@occlumency",
  },
}
```

## Componente de SEO

Crea un componente nuevo con esta plantilla inicial:

```jsx:title=src/components/SEO.js
import React from "react"
import { Helmet } from "react-helmet"
import PropTypes from "prop-types"
import { StaticQuery, graphql } from "gatsby"

const SEO = ({ title, description, image, pathname, article }) => ()

export default SEO

SEO.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string,
  image: PropTypes.string,
  pathname: PropTypes.string,
  article: PropTypes.bool,
}

SEO.defaultProps = {
  title: null,
  description: null,
  image: null,
  pathname: null,
  article: false,
}
```

**Nota:** los `propTypes` están incluidos en este ejemplo para ayudarte a asegurar que estás obteniendo todos los datos que necesitas en el componente, y sirven como una guía mientras desestructuras / usas estas _props_.

Como el componente de SEO también debería ser utilizable en otros archivos, por ejemplo un archivo plantilla, el componente acepta propiedades para las cuales estableces valores predeterminados en la sección `SEO.defaultProps`. De esta forma la información que colocas en `siteMetadata` se usa cada vez a menos que definas explícitamente la propiedad.

Ahora define la consulta y colócala en StaticQuery (también puedes guardar la consulta en una constante). También puedes crear un alias para los campos, de esta forma `title` se renombra a `defaultTitle`.

```jsx:title=src/components/SEO.js
const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery query={query} render={} />
)

export default SEO

const query = graphql`
  query SEO {
    site {
      siteMetadata {
        defaultTitle: title
        titleTemplate
        defaultDescription: description
        siteUrl: url
        defaultImage: image
        twitterUsername
      }
    }
  }
`
```

El siguiente paso consiste en desestructurar los datos de la consulta y crear un objeto que verifica si las _props_ fueron usadas — si no, los valores por defecto son utilizados. El alias de nombres es útil aquí: Evita las colisiones de nombres.

```jsx:title=src/components/SEO.js
const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={({
      site: {
        siteMetadata: {
          defaultTitle,
          titleTemplate,
          defaultDescription,
          siteUrl,
          defaultImage,
          twitterUsername,
        }
      }
    }) => {
      const seo = {
        title: title || defaultTitle,
        description: description || defaultDescription,
        image: `${siteUrl}${image || defaultImage}`,
        url: `${siteUrl}${pathname || '/'}`,
      }

      return ()
    }}
  />
)

export default SEO
```

El último paso es retornar estos datos con la ayuda de `Helmet`. Tu componente de SEO completo debería verse así:

```jsx:title=src/components/SEO.js
import React from "react"
import { Helmet } from "react-helmet"
import PropTypes from "prop-types"
import { StaticQuery, graphql } from "gatsby"

const SEO = ({ title, description, image, pathname, article }) => (
  <StaticQuery
    query={query}
    render={({
      site: {
        siteMetadata: {
          defaultTitle,
          titleTemplate,
          defaultDescription,
          siteUrl,
          defaultImage,
          twitterUsername,
        },
      },
    }) => {
      const seo = {
        title: title || defaultTitle,
        description: description || defaultDescription,
        image: `${siteUrl}${image || defaultImage}`,
        url: `${siteUrl}${pathname || "/"}`,
      }

      return (
        <>
          <Helmet title={seo.title} titleTemplate={titleTemplate}>
            <meta name="description" content={seo.description} />
            <meta name="image" content={seo.image} />
            {seo.url && <meta property="og:url" content={seo.url} />}
            {(article ? true : null) && (
              <meta property="og:type" content="article" />
            )}
            {seo.title && <meta property="og:title" content={seo.title} />}
            {seo.description && (
              <meta property="og:description" content={seo.description} />
            )}
            {seo.image && <meta property="og:image" content={seo.image} />}
            <meta name="twitter:card" content="summary_large_image" />
            {twitterUsername && (
              <meta name="twitter:creator" content={twitterUsername} />
            )}
            {seo.title && <meta name="twitter:title" content={seo.title} />}
            {seo.description && (
              <meta name="twitter:description" content={seo.description} />
            )}
            {seo.image && <meta name="twitter:image" content={seo.image} />}
          </Helmet>
        </>
      )
    }}
  />
)

export default SEO

SEO.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string,
  image: PropTypes.string,
  pathname: PropTypes.string,
  article: PropTypes.bool,
}

SEO.defaultProps = {
  title: null,
  description: null,
  image: null,
  pathname: null,
  article: false,
}

const query = graphql`
  query SEO {
    site {
      siteMetadata {
        defaultTitle: title
        titleTemplate
        defaultDescription: description
        siteUrl: url
        defaultImage: image
        twitterUsername
      }
    }
  }
`
```

## Ejemplos

También puedes poner los meta-tags de Facebook y Twitter en sus propios componentes, agregar favicons personalizados que se encuentran en tu carpeta `static`, y agregar datos de [schema.org](https://schema.org/) (Google usará eso para sus [Datos Estructurados](https://developers.google.com/search/docs/guides/intro-structured-data?hl=es-419)). Para ver cómo funciona, puedes echar un vistazo a estos dos ejemplos:

- [marisamorby.com](https://github.com/marisamorby/marisamorby.com/blob/master/packages/gatsby-theme-blog-sanity/src/components/seo.js)
- [gatsby-starter-prismic](https://github.com/LeKoArts/gatsby-starter-prismic/blob/master/src/components/SEO/SEO.jsx)

Como se mencionó al inicio también eres capaz de usar el componente en plantillas, como en [este ejemplo](https://github.com/jlengstorf/marisamorby.com/blob/6e86f845185f9650ff95316d3475bb8ac86b15bf/src/templates/post.js#L12-L18).
