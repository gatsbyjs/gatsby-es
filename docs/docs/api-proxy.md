---
title: "Filtrando peticiones a APIs en desarrollo"
---

## Recursos

Si no estas familiarizado con los ciclos de vida de Gatsby, revisa la vista general de [APIs de ciclo de vida de Gatsby](/docs/gatsby-lifecycle-apis/).

## Filtrando peticiones a APIs en desarrollo

De seguido la gente sirve una aplicación React desde el mismo _host_ y puerto que su
servidor _backend_.

Para indicarle al servidor de desarrollo que filtre cualquier petición no conocida a tu servidor API
en desarrollo, agrega un campo `proxy` a tu `gatsby-config.js`, por ejemplo:

```js:title=gatsby-config.js
module.exports = {
  proxy: {
    prefix: "/api",
    url: "http://dev-mysite.com",
  },
}
```

De esta manera, cuando en desarrollo tu hagas `fetch('/api/todos')`, el servidor de desarrollo
reconocerá que no es un recurso estático, y filtrará tu petición a
`http://dev-mysite.com/api/todos` como plan de contingencia.

Ten en mente que `proxy` solo tiene efecto en desarrollo (con `gatsby develop`), y depende de ti el asegurar que URLs como `/api/todos` apunten a
el lugar indicado en producción.

## Proxy avanzado

Algunas ocasiones necesitas acceso más granular/flexible a el servidor de desarrollo.
Gatsby expone el servidor de desarrollo [Express.js](https://expressjs.com/) a tu sitio `gatsby-config.js` donde tu
puedes agregar middleware de Express según necesites.

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

### Certificados con sello-propia

Si tu filtras a APIs locales con certificados con sello-propio, establece la opción `secure` a `false`.

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
