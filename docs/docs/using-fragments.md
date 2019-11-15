---
title: Usando Fragmentos
---

Los Fragmentos te permiten reutilizar partes de consultas GraphQL. También te permiten dividir consultas complejas en componentes más pequeños y fáciles de entender.

## Los bloques de construcción de un fragmento

Aquí está un ejemplo de un fragmento:

```graphql
fragment FragmentName on TypeName {
  field1
  field2
}
```

Un fragmento consiste en tres componentes:

1. `FragmentName`: el nombre del fragmento que será referenciado más tarde.
2. `TypeName`: el [GraphQL type](https://graphql.org/graphql-js/object-types/) de un objeto en el que se usará el fragmento. Este es importante porque sólo puede consultar los campos que realmente existen en un objeto determinado.
3. El cuerpo de la consulta. Puedes definir cualquier campo con cualquier nivel de anidamiento aquí, igual que lo haría en cualquier otra parte de una consulta GraphQL.

## Creando y usando un fragmento

Un fragmento puede ser creado dentro de cualquier consulta GraphQL, pero es una buena práctica crear la consulta por separado. Más consejos de organizacioón en [Conceptual Guide](/docs/querying-with-graphql/#fragments).

```jsx:title=src/components/IndexPost.jsx
import React from "react"
import { graphql } from "gatsby"

export default ( props ) => {
  return (...)
}

export const query = graphql`
  fragment SiteInformation on Site {
    siteMetadata {
      title
      siteDescription
    }
  }
`
```

Esto define un fragmento llamado `SiteInformation`. Ahora puede ser usado dentro de la consulta GraphQL de la página:

```jsx:title=src/pages/main.jsx
import React from "react"
import { graphql } from "gatsby"
import IndexPost from "../components/IndexPost"

export default ({ data }) => {
  return (
    <div>
      <h1>{data.site.siteMetadata.title}</h1>
      <p>{data.site.siteMetadata.siteDescription}</p>

      {/*
        Or you can pass all the data from the fragment
        back to the component that defined it
      */}
      <IndexPost siteInformation={data.site.siteMetadata} />
    </div>
  )
}

export const query = graphql`
  query {
    site {
      ...SiteInformation
    }
  }
`
```

Cuando compilas tu sitio, Gatsby preprocesa todas las consultas GraphQL que encuentra. Por lo tanto, cualquier archivo que se incluye en tu proyecto puede definir un snippet. Sin embargo, sólo las páginas pueden definir consultas GraphQL que realmente devuelven datos. Esto es por que podemos definir el fragmento en el archivo componente - en realidad no regresa ningún dato directamente.

## Otras lecturas

- [Consultar datos con GraphQL - Fragments](/docs/querying-with-graphql/#fragments)
- [Documentación GraphQL - Fragments](https://graphql.org/learn/queries/#fragments)
