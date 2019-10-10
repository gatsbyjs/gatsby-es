---
El titulo: Adición de página metadata
---

Si has corrido una [auditoría con Lighthouse](/docs/audit-with-lighthouse/), usted puede haber notado un deslucido score en el "SEO" categoría. Vamos a abordar el tema de cómo puede mejorar la puntuación.

La adición metadata a páginas (como un título o descripción) es clave en la ayuda de motores de búsqueda como Google a entender su contenido y decidir cuando revestirlo en resultados de la búsqueda.

[React Helmet](https://github.com/nfl/react-helmet) es un paquete que proporciona un React el componente interfaz para administrar sus [documento cabeza].(https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

Gatsby's [react helmet plugin](/packages/gatsby-plugin-react-helmet/) proporciona la deserción en soporte para servidor procese datos agregados con React Helmet. Usando el plugin, los atributos se agregan a React Helmet será añadido a la páginas HTML estáticas que Gatsby compilaciones.

### La utilización `React Helmet` y `gatsby-plugin-react-helmet`

1. Instale ambos paquetes:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2. Agregue el plugin a la matriz `plugins` en su archivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [`gatsby-plugin-react-helmet`]
}
```

3. La utilización `React Helmet` en tus páginas:

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

> 💡 El susodicho ejemplo es del [React Helmet docs](https://github.com/nfl/react-helmet#example). ¡Compruebe a aquellos para más!

También puede estar interesado en el registro de salida del doctor en [adición de un componente SEO](/docs/add-seo-component/).
