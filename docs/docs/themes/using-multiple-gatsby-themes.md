---
título: Usando de múltiples temas de Gatsby
---

Gatsby temas están destinados a ser componible. Esto significa que puede instalar temas múltiples el uno junto al otro.

La `gatsby-starter-theme` compone dos temas de Gatsby: `gatsby-theme-blog` y `gatsby-theme-notes`

```shell
gatsby new my-notes-blog https://github.com/gatsbyjs/gatsby-starter-theme
```

El inicio incluye ambos paquetes de tema (`gatsby-theme-blog` y `gatsby-theme-notes`) en el archivo `gatsby-config.js` del starter.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-notes`,
      options: {
        mdx: true,
        basePath: `/notes`,
      },
    },
    // con gatsby-plugin-theme-ui, el último tema en la configuración
    // anulará el contexto theme-ui de otros temas
    { resolve: `gatsby-theme-blog` },
  ],
  siteMetadata: {
    title: `Shadowed Site Title`,
  },
}
```

En la configuración predeterminada, se servirá un blog desde la ruta raíz (`/`), y el contenido de las notas se servirá desde `/notes`.

Ejecute `gatsby develop` para iniciar un servidor de desarrollo y ver si es el sitio:

![The homepage of the site created by gatsby-theme-starter](../images/gatsby-theme-starter-home.png)

![The `notes` route of a site created by gatsby-theme starter](../images/gatsby-theme-starter-notes.png)

## El tutorial

Para ver un tutorial paso a paso, consulte el tutorial ["Uso de varios temas juntos"](/tutorial/using-multiple-themes-together).
