---
title: "Rutas solo para el cliente & Autenticación de usuario"
---

A menudo, deseas crear un sitio con partes solamente para el lado del cliente, que te permiten filtrarlos por autenticación o cargar contenido diferente basado en los parámetros de la URL.

## Entendiendo las rutas solo para cliente

Un ejemplo clásico sería un sitio que tiene una página de destino, varias páginas de marketing, una página de inicio de sesión y luego una sección de aplicación para usuarios que han iniciado sesión. La sección de inicio de sesión no necesita ser procesada por el servidor, ya que todos los datos se cargarán en vivo desde tu API después de que el usuario inicie sesión. Por lo tanto, tiene sentido que esta parte de tu sitio sea solo para el lado del cliente.

Las rutas solo para cliente existirán solo en el cliente y no corresponderán a archivos `index.html` en los archivos de compilado de la aplicación. Sí te gustaría permitir a los usuarios visitar rutas solo para cliente directamente, necesitas [configurar tu sitio para manejar esas rutas](#handling-client-only-routes-with-gatsby) apropiadamente. O, sí tienes control sobre la configuración del archivo del servidor por ti mismo (en lugar de usar otro _host_ de archivos estáticos como Netlify), puedes [configurar el servidor](#configuring-and-handling-client-only-routes-on-a-server) para manejar estas rutas.

Un sitio de muestra se puede configurar así:

![Sitio con una página principal estática y rutas solo para cliente](./images/client-only-routes.png)

Gatsby convierte los componentes en la carpeta `pages` en archivos HTML estáticos para la página _Home_ y la página _App_. Un `<Router />` es añadido a la página _App_ para que los componentes de perfil y detalles puedan ser renderizados desde la página _App_; estos no tienen archivos estáticos compilados por ellos ya que solo existen en el lado del cliente. La página del perfil puede hacer un `POST` de datos sobre el usuario desde la API, y la página de detalles puede cargar datos dinámicamente sobre el usuario con un _ID_ específico desde la API.

# Manejando rutas solo para cliente con Gatsby

Gatsby usa [@reach/router](https://reach.tech/router/) debajo del capó, y es el enfoque recomendado para crear rutas solo para cliente.

Primero necesitas configurar rutas en una página que está hecha con Gatsby:

```jsx:title=src/pages/app.js
import React from "react"
import { Router } from "@reach/router" // highlight-line
import Layout from "../components/Layout"
import Profile from "../components/Profile"
import Details from "../components/Details"
import Login from "../components/Login"
import Default from "../components/Default"

const App = () => {
  return (
    <Layout>
      // highlight-start
      <Router basepath="/app">
        <Profile path="/profile" />
        <Details path="/details" />
        <Login path="/login" />
        <Default path="/" />
      </Router>
      // highlight-end
    </Layout>
  )
}

export default App
```

Con rutas anidadas debajo del `<Router />` de `Reach Router`, [renderizará el componente de la ruta que corresponda a la `ruta`](https://reach.tech/router/api/Router). En el caso de la ruta `/app/profile`, el componente `profile` será renderizado, ya que su prefijo coincide con la ruta `/app`, y la parte restante es idéntica a la ruta de su hijo.

### Ajustando rutas de cuenta para usuarios autenticados

Con la [autenticación configurada](/docs/building-a-site-with-authentication) en tu sitio, puedes crear un componente como `<PrivateRoute/>` para expandir el ejemplo de arriba y filtrar contenido:

```jsx:title=src/pages/app.js
import React from "react"
import { Router } from "@reach/router"
import Layout from "../components/Layout"
import Profile from "../components/Profile"
import Details from "../components/Details"
import Login from "../components/Login"
import Default from "../components/Default"
import PrivateRoute from "../components/PrivateRoute" // highlight-line

const App = () => {
  return (
    <Layout>
      <Router basepath="/app">
        // highlight-start
        <PrivateRoute path="/profile" component={Profile} />
        <PrivateRoute path="/details" component={Details} />
        // highlight-end
        <Login path="/login" />
        <Default path="/" />
      </Router>
    </Layout>
  )
}

export default App
```

El componente `<PrivateRoute />` se vería similar a algo como este (tomado del [Tutorial de Autenticación](/tutorial/authentication-tutorial/#controlling-private-routes), que implementa este comportamiento):

```jsx:title=src/components/PrivateRoute.js
// import ...
import React, { Component } from "react"
import { navigate } from "gatsby"
import { isLoggedIn } from "../services/auth"

const PrivateRoute = ({ component: Component, location, ...rest }) => {
  if (!isLoggedIn() && location.pathname !== `/app/login`) {
    navigate("/app/login")
    return null
  }

  return <Component {...rest} />
}

export default PrivateRoute
```

### Configurando páginas con `matchPath`

Para asegurarte de que los usuarios puedan navegar a rutas solo para cliente directamente, las páginas en tu sitio necesitan tener el [parámetro `matchPath`](/docs/gatsby-internals-terminology/#matchpath) configurado. Agrega el siguiente código al archivo `gatsby-node.js` de tu sitio:

```javascript:title=gatsby-node.js
// Implementa la API “onCreatePage” de Gatsby. Esto se
// llama después de crear cada página.
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage } = actions
  
  // Solo actualiza la página `/app`.
  if (page.path.match(/^\/app/)) {
    // page.matchPath es una llave especial que es usada para hacer coincidir páginas
    // con rutas correspondientes solo en el cliente.
    page.matchPath = "/app/*"

    // Actualiza la página.
    createPage(page)
  }
}
```

> 💡 Nota: También hay un plugin para simplificar la creación de rutas solo para el lado del cliente en tu sitio
> [gatsby-plugin-create-client-paths](/packages/gatsby-plugin-create-client-paths/).

El código de arriba (así como también el plugin `gatsby-plugin-create-client-paths`) actualiza la página `/app` en tiempo de compilación para agregar el parámetro `matchPath` en el objeto para asegurarse de que las páginas configuradas (en este caso, todo después de `/app`, cómo `/app/dashboard` o `/app/user`) puedan ser navegadas a ellas por `Reach Router`.

_Sin_ esta configuración hecha, un usuario que haga clic en un enlace a `<tusitio.com>/app/user` será llevado a la página estática de `/app` en lugar del componente o página que configuraste para `/app/user`.

> Consejo: Para aplicaciones con enrutamiento complejo, es posible que desees anular el comportamiento de desplazamiento predeterminado de Gatsby con la API del navegador [shouldUpdateScroll](/docs/browser-apis/#shouldUpdateScroll).

## Configurando y manejando rutas solo para cliente en un servidor

Sí estás almacenando en tu propio servidor, puedes optar por configurar el servidor para manejar las rutas solo para cliente en lugar de usar el método `matchPath` explicado arriba.

Considera el siguiente `router` y ruta como ejemplo:

```jsx:title=src/pages/app.js
<Router basepath="/app">
  <Route path="/why-gatsby-is-awesome" />
</Router>
```

En este ejemplo con un `router` y una sola ruta para `/app/why-gatsby-is-awesome/`, el servidor no sería capaz de completar la solicitud ya que `why-gatsby-is-awesome` es una ruta solo para cliente. No tiene un archivo HTML correspondiente en el servidor. El archivo encontrado en `/app/index.html` en el servidor contiene todo el código para manejar las rutas de la página después de `/app`.

Un patrón a seguir, agnóstico de la tecnología del servidor, es mirar por estas rutas en expecífico y retornar el archivo HTML apropiado.

En este ejemplo, cuando se hace una solicitud `GET` a `/app/why-gatsby-is-awesome`, el servidor debería responder con `/app/index.html` y dejar que el cliente maneje el renderizado de la ruta que coincida. Es importante recordar que el código de respuesta debería ser un **200** (un OK) y no un **301** (una redirección).

Un resultado de este método es que el cliente es completamente indiferente a la lógica del servidor, desacoplándolo de Gatsby.

## Recursos adicionales

- [Repo de ejemplo de Gatsby: "Autenticación simple"](https://github.com/gatsbyjs/gatsby/blob/master/examples/simple-auth/) - un demo implementando autenticación de usuario y restringiendo rutas solo para cliente
- [Versión en vivo del ejemplo "Autenticación simple"](https://simple-auth.netlify.com/)
- [La tienda de Gatsby](https://github.com/gatsbyjs/store.gatsbyjs.org) que también implementa un flujo de autenticación
