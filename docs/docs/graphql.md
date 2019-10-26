---
title: GraphQL y Gatsby
overview: true
---

Cuando desarrolles con Gatsby, accederás a tus datos por medio del lenguaje de consulta [GraphQL](http://graphql.org/). GraphQL te permite expresar tus necesidades de datos declarativamente. Esto es hecho con `consultas`. Las consultas son la representación de los datos que necesitas. Una consulta tiene la siguiente forma:

```graphql
{
  site {
    siteMetadata {
      title
    }
  }
}
```

La cual devuelve:

```json
{
  "site": {
    "siteMetadata": {
      "title": "A Gatsby site!"
    }
  }
}
```

Observa como la estructura de la consulta concuerda con la estructura del JSON recibido. Esto es posible porque, en GraphQL, tu consulta se empareja con un `schema`, la cual, es la representación de tus datos disponibles. No te preocupes por como el esquema llega desde ahora. Gatsby se encarga de organizar todos tus datos por ti, y los hace reconocibles con una herramienta llamada GraphiQL. GraphiQL es una interfaz gráfica, que te permite 1) Hacer consultas de tus datos en el navegador. 2) Inspeccionar la estructura de datos disponible, a través de un explorador de tipos de dato.

Si quieres saber más acerca de GraphQL, puedes leer más acerca de [porque Gatsby lo usa](/docs/why-gatsby-uses-graphql) y revisar esta [guía conceptual](/docs/querying-with-graphql) sobre consultas de datos con GraphQL.

<GuideList slug={props.slug} />
