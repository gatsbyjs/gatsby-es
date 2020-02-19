---
title: "Filtrando peticiones a APIs en desarrollo"
---

## Recursos

Si no estás familiarizado con los ciclos de vida de Gatsby, revisa la vista general de [APIs de ciclo de vida de Gatsby](/docs/gatsby-lifecycle-apis/).

## Filtrando peticiones a APIs en desarrollo

<<<<<<< HEAD
La gente a menudo sirve una aplicación React desde el mismo _host_ y puerto que su
servidor _backend_.

Para indicarle al servidor de desarrollo que filtre cualquier petición no conocida a tu servidor API
en desarrollo, agrega un campo `proxy` a tu `gatsby-config.js`, por ejemplo:
=======
People often serve the frontend React app from the same host and port as their backend implementation.

To tell the development server to proxy any unknown requests to your API server in development, add a `proxy` field to your `gatsby-config.js`, for example:
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```javascript:title=gatsby-config.js
module.exports = {
  proxy: {
    prefix: "/api",
    url: "http://dev-mysite.com",
  },
}
```

<<<<<<< HEAD
De esta manera, cuando en desarrollo tu hagas `fetch('/api/todos')`, el servidor de desarrollo
reconocerá que no es un recurso estático, y filtrará tu petición a
`http://dev-mysite.com/api/todos` como plan de contingencia.

Ten en mente que `proxy` solo tiene efecto en desarrollo (con `gatsby develop`), y depende de ti el asegurar que URLs como `/api/todos` apunten a
el lugar indicado en producción.
=======
or:

```js:title=gatsby-config.js
module.exports = {
  proxy: [
    {
      prefix: "/api",
      url: "http://dev-mysite.com",
    },
    {
      prefix: "/api2",
      url: "http://dev2-mysite.com",
    },
  ],
}
```

This way, when you `fetch('/api/todos')` in development, the development server will recognize that it’s not a static asset, and will proxy your request to `http://dev-mysite.com/api/todos` as a fallback.

Keep in mind that `proxy` only has effect in development (with `gatsby develop`), and it is up to you to ensure that URLs like `/api/todos` point to the right place in production.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Proxy avanzado

<<<<<<< HEAD
Algunas ocasiones necesitas acceso más granular/flexible a el servidor de desarrollo.
Gatsby expone el servidor de desarrollo [Express.js](https://expressjs.com/) a tu sitio `gatsby-config.js` donde tú
puedes agregar _middleware_ de Express según necesites.
=======
Sometimes you need more granular/flexible access to the development server. Gatsby exposes the [Express.js](https://expressjs.com/) development server to your site's `gatsby-config.js` where you can add Express middleware as needed.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```javascript:title=gatsby-config.js
var proxy = require("http-proxy-middleware")

module.exports = {
  developMiddleware: app => {
    app.use(
      "/.netlify/functions/",
      proxy({
        target: "http://localhost:9000",
        pathRewrite: {
          "/.netlify/functions/": "",
        },
      })
    )
  },
}
```

Ten en mente que _middleware_ solo tiene efecto en desarrollo (con `gatsby develop`).

### Certificados con sello-propio

Si filtras a APIs locales con certificados con sello-propio, establece la opción `secure` a `false`.

```javascript:title=gatsby-config.js
var proxy = require("http-proxy-middleware")
module.exports = {
  developMiddleware: app => {
    app.use(
      "/.netlify/functions/",
      proxy({
        target: "http://localhost:9000",
        secure: false, // Do not reject self-signed certificates.
        pathRewrite: {
          "/.netlify/functions/": "",
        },
      })
    )
  },
}
```
