---
title: Agregar metadatos de página
---

Si ha ejecutado un [audit with Lighthouse](/docs/audit-with-lighthouse/), es posible que hayas notado una puntuación poco brillante en la categoría «SEO». Vamos a abordar cómo puedes mejorar esa puntuación.

Agregar metadatos a las páginas (como un título o una descripción) es clave para ayudar a los motores de búsqueda como Google a comprender tu contenido y decidir cuándo hacerlo en los resultados de búsqueda.

[React Helmet](https://github.com/nfl/react-helmet) es un paquete que proporciona una interfaz de componente React para que pueda administrar su [document head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

Gatsby's [react helmet plugin](/packages/gatsby-plugin-react-helmet/) proporciona soporte directo para los datos de representación del servidor agregados con React Helmet. Usando el plugin, los atributos que agregue a React Helmet se agregarán a las páginas HTML estáticas que Gatsby construye.

### Usando  `React Helmet` y  `gatsby-plugin-react-helmet`

1. Instalar ambos paquetes:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2. Agregue el plugin a la matriz `plugins` en su archivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [`gatsby-plugin-react-helmet`]
}
```

3. Uso `React Helmet` en sus páginas:

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

> 💡 El ejemplo anterior es de la [React Helmet docs](https://github.com/nfl/react-helmet#example). ¡Échale un vistazo para más!

También puede estar interesado en consultar el documento en [adding an SEO component](/docs/add-seo-component/).
