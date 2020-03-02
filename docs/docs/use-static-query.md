---
title: Consultando información en componentes utilizando useStaticQuery Hook
---

Gatsby v2.1.0 introdujo `useStaticQuery`, una nueva característica de Gatsby que provee la habilidad de usar [React Hook](https://reactjs.org/docs/hooks-intro.html) para hacer consultas con GraphQL en _build time_.

Al igual que el componente [StaticQuery](/docs/static-query/), permite que tu componente de React pueda recibir información via una consulta de GraphQL que es parseada, evaluada e injectada dentro del componente. ¡Sin embargo, `useStaticQuery` es un hook más que un componente que toma propiedades de rendereo!

En esta guía, vas a transitar por un ejemplo utilizando `useStaticQuery`. Si todavía no estas familiarizado con las consultas estáticas en Gatsby, quizás deberíasa darle un vistazo a [la diferencia entre una consulta estática y una consulta de página](/docs/static-query/#how-staticquery-differs-from-page-query).

## Cómo usar useStaticQuery en componentes

> 💡 Vas a necesitar React y ReactDOM 16.8.0 or mayor para usar `useStaticQuery`.
>
> 📦 `npm install react@^16.8.0 react-dom@^16.8.0`

`useStaticQuery` es un React Hook. Todas las [Reglas de Hooks](https://reactjs.org/docs/hooks-rules.html) aplican.

Esto toma tus consultas de GraphQL y retorna la información solicitada. ¡Simplemente así!

### Ejemplo básico

Vamos a crear componente `Header` que va a consultar por el título del sitio desde `gatsby-config.js`:

```jsx:title=src/components/header.js
import React from "react"
import { useStaticQuery, graphql } from "gatsby"

export default () => {
  const data = useStaticQuery(graphql`
    query HeaderQuery {
      site {
        siteMetadata {
          title
        }
      }
    }
  `)

  return (
    <header>
      <h1>{data.site.siteMetadata.title}</h1>
    </header>
  )
}
```

### Componiendo un `useStaticQuery` hooks personalizado

Uno de las características más convincentes de hooks is the ability to compose and re-use these blocks of functionality. `useStaticQuery` is a hook. Therefore, using `useStaticQuery` allows us to compose and re-use blocks of reusable functionality. Perfect!

A classic example is to create a `useSiteMetadata` hook which will provide the `siteMetadata` to be re-used in any component. It looks something like:

```jsx:title=src/hooks/use-site-metadata.js
import { useStaticQuery, graphql } from "gatsby"

export const useSiteMetadata = () => {
  const { site } = useStaticQuery(
    graphql`
      query SiteMetaData {
        site {
          siteMetadata {
            title
            siteUrl
            headline
            description
            image
            video
            twitter
            name
            logo
          }
        }
      }
    `
  )
  return site.siteMetadata
}
```

Then just import your newly created hook, like so:

```jsx:title=src/pages/index.js
import React from "react"
import { useSiteMetadata } from "../hooks/use-site-metadata"

export default () => {
  const { title, siteUrl } = useSiteMetadata()
  return <h1>welcome to {title}</h1>
}
```

## Known Limitations

- `useStaticQuery` does not accept variables (hence the name "static"), but can be used in _any_ component, including pages
- Because of how queries currently work in Gatsby, we support only a single instance of `useStaticQuery` in a file
