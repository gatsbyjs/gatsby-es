---
title: Creando Páginas 404 Prefijadas en Diferentes Idiomas
---

Usando la API [`onCreatePage`](/docs/node-apis/#onCreatePage) en el archivo `gatsby-node.js` de tu proyecto, es posible crear diferentes páginas 404 para diferentes URL prefijadas, como `/en/`.

En el siguiente ejemplo, vamos a crear una página 404 en inglés en `src/pages/en/404.js`, y una página 404 en alemán en `/src/pages/de/404.js`. Éste es un ejemplo sencillo:

```javascript:title=src/pages/en/404.js
import React from "react"
import Layout from "../../components/layout"

export default () => (
  <Layout>
    <h1>Page Not Found</h1>
    <p>Oops, we couldn't find this page!</p>
  </Layout>
)
```

```javascript:title=src/pages/de/404.js
import React from "react"
import Layout from "../../components/layout"

export default () => (
  <Layout>
    <h1>Seite nicht gefunden</h1>
    <p>Ups, wir konnten diese Seite nicht finden!</p>
  </Layout>
)
```

Ahora, abre el `gatsby-node.js` de tu proyecto y añade el siguiente código:

```javascript:title=gatsby-node.js
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage, deletePage } = actions

  // Comprueba si la página es una 404 localizada
  if (page.path.match(/^\/[a-z]{2}\/404\/$/)) {
    const oldPage = { ...page }

    // Obtiene el idioma de la ruta y empareja todas las rutas
    // que empiecen con este código (aparte de otras rutas válidas)
    const langCode = page.path.split(`/`)[1]
    page.matchPath = `/${langCode}/*`

    // Recrea la página modificada
    deletePage(oldPage)
    createPage(page)
  }
}
```

Ahora, cada vez que Gatsby crea una página, comprobará si la página es una 404 localizada con el formato `/XX/404/`. Si ese es el caso, entonces obtendrá el código de idioma y emparejará todas las rutas que empiecen con ese código, aparte de otras rutas válidas. Esto significa que cuando visites una página que no existe en tu sitio, cuya ruta empiece por `/en/` o `/de/` (p.e. `/en/esto-no-existe`), tu página 404 localizada será mostrada en su lugar.

Para obtener mejores resultados, debes configurar tu servidor para que sirva esas páginas 404 de la misma manera. Por ejemplo, para `/en/<ruta no existente>`, tu servidor debe servir la página `/en/404/`. De lo contrario, verás la página 404 por defecto durante un instante hasta que cargue el _runtime_ de Gatsby. Si estás usando Netlify, puedes usar [`gatsby-plugin-netlify`](/packages/gatsby-plugin-netlify/) para hacer esto automáticamente. Ten en cuenta que aun deberás crear una página 404 por defecto (normalmente en `src/pages/404.js`) para gestionar las rutas sin prefijos, p.e. `https://ejemplo.com/esto-no-existe`.
