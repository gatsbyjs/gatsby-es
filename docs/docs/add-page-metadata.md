---
title: Agregando metadatos a las páginas
---

Si has realizado una [auditoría con Lighthouse](/docs/audit-with-lighthouse/), es posible que hayas notado una puntuación mediocre en la categoría "SEO". Veamos cómo se puede mejorar esta puntuación.

Agregando metadatos a las páginas (como un título o una descripción) es clave para ayudar a los motores de búsqueda como Google a comprender el contenido y decidir cuándo mostrarlo en sus resultados de búsqueda.

[React Helmet](https://github.com/nfl/react-helmet) es un paquete que proporciona una interfaz al componente React para que pueda administrar el tag [head del documento](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

El plugin [react helmet](/packages/gatsby-plugin-react-helmet/) para Gatsby proporciona soporte directo para información de render de servidor agregados con React Helmet. Usando el complemento, los atributos que agregue a React Helmet se agregarán a las páginas HTML estáticas que Gatsby compila.

### Usando `React Helmet` y `gatsby-plugin-react-helmet`

1. Instala ambos paquetes:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2. Agrega el complemento al array `plugins` en tu archivo` gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [`gatsby-plugin-react-helmet`]
}
```

3. Usa `React Helmet` en tus páginas:

```jsx
import React from "react"
import { Helmet } from "react-helmet"

class Application extends React.Component {
  render() {
    return (
      <div className="application">
        {/* highlight-start */}
        <Helmet>
          <meta charSet="utf-8" />
          <title>My Title</title>
          <link rel="canonical" href="http://mysite.com/example" />
        </Helmet>
        {/* highlight-end */}
      </div>
    )
  }
}
```

> 💡 El ejemplo anterior es de la [documentación de React Helmet](https://github.com/nfl/react-helmet#example). ¡Échales un vistazo para más!

También puedes estar interesado en consultar el documento sobre [agregar un componente de SEO](/docs/add-seo-component/).
