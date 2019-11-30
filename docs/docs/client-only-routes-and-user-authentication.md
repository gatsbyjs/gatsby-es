---
title: "Rutas solo para el cliente & Autenticación de Usuario"
---

A menudo, deseas crear un sitio con partes solamente para el lado del cliente que están protegidas con autenticación.

Un ejemplo clásico sería un sitio que tiene una página de destino, varias páginas de marketing, una página de inicio de sesión y luego una sección de aplicación para usuarios que han iniciado sesión. La sección de inicio de sesión no necesita ser procesada por el servidor, ya que todos los datos se cargarán en vivo desde tu API después de que el usuario inicie sesión. Por lo tanto, tiene sentido que esta parte de tu sitio sea solo para el lado del cliente.

Gatsby usa [@reach/router](https://reach.tech/router/) debajo del capó. Deberías usar @reach/router para crear rutas solo para el lado del cliente.

Estas rutas existirán sólo en el lado del cliente y no se corresponderán con archivos index.html en los recursos construidos por una aplicación. Si deseas que los usuarios del sitio puedan visitar las rutas de los clientes directamente, deberás configurar tu servidor para manejar esas rutas de manera adecuada.

Para crear rutas solo para el lado del cliente, agrega el siguiente código al archivo `gatsby-node.js` de tu sitio:

```javascript:title=gatsby-node.js
// Implementa la API “onCreatePage” de Gatsby. Esto se
// llama después de que cada página se carga.
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage } = actions

  // page.matchPath es una calve especial que se utiliza para hacer coincidir páginas
  // solo en el cliente.
  if (page.path.match(/^\/app/)) {
    page.matchPath = "/app/*"

    // Actualiza la página.
    createPage(page)
  }
}
```

> 💡 Nota: También hay un plugin para simplificar la creación de rutas solo para el lado del cliente en tu sitio
> [gatsby-plugin-create-client-paths](/packages/gatsby-plugin-create-client-paths/).

> Tip: Para aplicaciones con enrutamiento complejo, es posible que desees anular el comportamiento de desplazamiento predeterminado de Gatsby con la API del navegador [shouldUpdateScroll](/docs/browser-apis/#shouldUpdateScroll).

Consulta el [sitio de ejemplo de "autenticación simple"](https://github.com/gatsbyjs/gatsby/blob/master/examples/simple-auth/) para ver una demostración que implementa la autenticación de usuarios y rutas restringidas solo para el lado del cliente.
