---
título: Crear un sitio con autenticación de usuario
---

A veces, debe crear un sitio con contenido cerrado, disponible solo para usuarios autenticados. Con Gatsby, puede lograr esto usando el concepto de [rutas solo para clientes](/docs/building-apps-with-gatsby/#Client-only-routes), para definir qué páginas puede ver un usuario solo después de iniciar sesión.

## Prerrequisitos

Ya debería haber configurado su entorno para poder usar el `gatsby-cli`. Un buen punto de partida es el [tutorial principal](/tutorial).

## Aviso de seguridad

En producción, debe usar una solución probada y sólida para manejar la autenticación. [Auth0](https://www.auth0.com), [Firebase](https://firebase.google.com) y [Passport.js](http://passportjs.org) son buenos ejemplos. Este tutorial solo cubrirá el flujo de trabajo de autenticación, pero debe tomar la seguridad de su aplicación lo más en serio posible.

## Construyendo tu aplicación Gatsby

Comience creando un nuevo proyecto de Gatsby utilizando el proyecto `hello-world` de partida:

```shell 
gatsby new gatsby-auth gatsbyjs/gatsby-starter-hello-world
cd gatsby-auth
```

Cree un nuevo componente para contener los enlaces. Por ahora, actuará como marcador de posición:

```jsx: title=src/components/nav-bar.js
import React from "react"
import { Link } from "gatsby"

export default () => (
  <div
    style={{
      display: "flex",
      flex: "1",
      justifyContent: "space-between",
      borderBottom: "1px solid #d1c1e0",
    }}
  >
    <span>You are not logged in</span>

    <nav>
      <Link to="/">Home</Link>
      {` `}
      <Link to="/">Profile</Link>
      {` `}
      <Link to="/">Logout</Link>
    </nav>
  </div>
)
```

Y cree el componente plantilla que envolverá todas las páginas y mostrará la barra de navegación:

```jsx:title=src/components/layout.js
import React from "react"

import NavBar from "./nav-bar"

const Layout = ({ children }) => (
  <>
    <NavBar />
    {children}
  </>
)

export default Layout
```

Por último, cambie la página de inicio para usar el componente plantilla:

```jsx:title=src/pages/index.js
import React from "react"

import Layout from "../components/layout" // highlight-line

// highlight-start
export default () => (
  <Layout>
    <h1>Hello world!</h1>
  </Layout>
)
// highlight-end
```

## Servicio de autenticación

Para este tutorial, utilizará un usuario/contraseña codificados. Cree la carpeta `src/services` y añada el siguiente contenido al archivo `auth.js`:

```javascript:title=src/services/auth.js
export const isBrowser = () => typeof window !== "undefined"

export const getUser = () =>
  isBrowser() && window.localStorage.getItem("gatsbyUser")
    ? JSON.parse(window.localStorage.getItem("gatsbyUser"))
    : {}

const setUser = user =>
  window.localStorage.setItem("gatsbyUser", JSON.stringify(user))

export const handleLogin = ({ username, password }) => {
  if (username === `john` && password === `pass`) {
    return setUser({
      username: `john`,
      name: `Johnny`,
      email: `johnny@example.org`,
    })
  }

  return false
}

export const isLoggedIn = () => {
  const user = getUser()

  return !!user.username
}

export const logout = callback => {
  setUser({})
  callback()
}
```

## Crear rutas solo para clientes

Al comienzo de este tutorial, creaste un sitio Gatsby "hello world", que incluye la biblioteca `@reach/router`. Ahora, utilizando la biblioteca [@reach/router](https://reach.tech/router/), puede crear rutas disponibles solo para los usuarios registrados. Gatsby utiliza esta biblioteca internamente, por lo que ni siquiera tiene que instalarla.

Primero, cree `gatsby-node.js` en el directorio raíz de su proyecto. Definirá que cualquier ruta que comience con `/app/` es parte de su contenido restringido y la página se creará a bajao demanda:

// Implemente la API de Gatsby "onCreatePage". Esto es
// se llama después de crear cada página.

```javascript:title=gatsby-node.js
// Implementa la API de Gatsby “onCreatePage”.
// Se llamará tras crear cada página
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage } = actions

  // page.matchPath es una clave especial para
  // comprobar coincidencias en el cliente
  if (page.path.match(/^\/app/)) {
    page.matchPath = "/app/*"

    // Actualiza la página
    createPage(page)
  }
}
```

> Nota: Hay un complemento conveniente que hace esta tarea por tí: [gatsby-plugin-create-client-paths](/packages/gatsby-plugin-create-client-paths)

Ahora, debe crear una página genérica que tendrá la tarea de generar el contenido restringido:

```jsx:title=src/pages/app.js
import React from "react"
import { Router } from "@reach/router"
import Layout from "../components/layout"
import Profile from "../components/profile"
import Login from "../components/login"

const App = () => (
  <Layout>
    <Router>
      <Profile path="/app/profile" />
      <Login path="/app/login" />
    </Router>
  </Layout>
)

export default App
```

