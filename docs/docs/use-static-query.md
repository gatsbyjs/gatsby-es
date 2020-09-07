---
Título: Consultando información en componentes utilizando useStaticQuery Hook
---

Gatsby v2.1.0 introdujo `useStaticQuery`, una nueva característica de Gatsby que provee la habilidad de usar [React Hook](https://reactjs.org/docs/hooks-intro.html) para hacer consultas con GraphQL en _build time_.

Al igual que el componente [StaticQuery](/docs/static-query/), permite que tus componentes de React puedan recibir información vía una consulta de GraphQL que será parseada, evaluada e injectada dentro del componente. Sin embargo, ¡`useStaticQuery` es un hook más que un componente que toma propiedades de rendereo!

En esta guía, veremos un ejemplo de uso de `useStaticQuery`. Si todavía no estas familiarizado con las consultas estáticas en Gatsby, quizás deberías darle un vistazo a [la diferencia entre una consulta estática y una consulta de página](/docs/static-query/#how-staticquery-differs-from-page-query).

## Cómo usar useStaticQuery en componentes

> 💡 Vas a necesitar React y ReactDOM 16.8.0 o mayor para usar `useStaticQuery`.
>
> 📦 `npm install react@^16.8.0 react-dom@^16.8.0`

`useStaticQuery` es un React Hook. Todas las [Reglas de Hooks](https://es.reactjs.org/docs/hooks-rules.html) aplican.

Esto toma tus consultas de GraphQL y retorna la información solicitada. ¡Así de simple!

### Ejemplo básico

Creamos un componente `Header` que consulte por el título del sitio desde `gatsby-config.js`:

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

### Componiendo hooks de `useStaticQuery` personalizados

Uno de las características más convincentes de hooks es la habilidad de componer y reutilizar estos bloques de funcionalidad. `useStaticQuery` es un hook. Por lo tanto, usar `useStaticQuery` nos permite componer y reutilizar bloques de funcionalidades reutilizable. ¡Perfecto!

Un ejemplo clásico es crear un `useSiteMetadata` hook el cuál permitira proveer al `siteMetadata` ser reutilizado en cualquier componente. Esto se ve algo así:

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

Entonces solamente importamos el nuevo hook creado, así:

```jsx:title=src/pages/index.js
import React from "react"
import { useSiteMetadata } from "../hooks/use-site-metadata"

export default () => {
  const { title, siteUrl } = useSiteMetadata()
  return <h1>Bienvenido a {title}</h1>
}
```

## Limitaciones a considerar

- `useStaticQuery` no acepta variables (por eso el nombre "static"), pero puede ser usado en _cualquier_ componente, incluido páginas.
- Debido a como funcionan las consultas actualmente en Gatsby, nosotros solamente damos soporte a una sola instancia de `useStaticQuery` en un archivo.
