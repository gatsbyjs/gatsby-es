---
título: Usar múltiples temas de Gatsby
---

Los temas Gatsby están destinados a ser combinados. Esto significa que puedes instalar varios temas el uno junto al otro.

El `gatsby-starter-theme` se compone de dos temas de Gatsby: `gatsby-theme-blog` y `gatsby-theme-notes`

```shell
gatsby new my-notes-blog https://github.com/gatsbyjs/gatsby-starter-theme
```

El starter incluye ambos paquetes de tema (`gatsby-theme-blog` y `gatsby-theme-notes`) en el archivo `gatsby-config.js` del starter.

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

Con la configuración predeterminada, se servirá un blog desde la ruta root (`/`), y el contenido de las notas se servirá desde `/notes`.

Ejecuta `gatsby develop` para iniciar un servidor de desarrollo y ver el sitio:

![The homepage of the site created by gatsby-theme-starter](../images/gatsby-theme-starter-home.png)

![The `notes` route of a site created by gatsby-theme starter](../images/gatsby-theme-starter-notes.png)

## El tutorial

Para ver un tutorial paso a paso, consulta el tutorial ["Usar varios temas juntos"](/tutorial/using-multiple-themes-together).
