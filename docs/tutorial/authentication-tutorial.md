---
title: Crear un sitio con autenticación de usuarios
---

A veces, debes crear un sitio con contenido cerrado, disponible solo para usuarios autenticados. Con Gatsby, puedes lograr esto usando el concepto de [rutas únicas del cliente](/docs/building-apps-with-gatsby/#client-only-routes), para definir qué páginas puede ver un usuario solo después de iniciar sesión.

## Prerrequisitos

Ya deberías haber configurado tu entorno para poder usar `gatsby-cli`. Un buen punto de partida es el [tutorial principal](/tutorial).

## Aviso de seguridad

En producción, deberías usar soluciones probadas y robustas para manejar la autenticación. [Auth0](https://www.auth0.com), [Firebase](https://firebase.google.com) y [Passport.js](http://passportjs.org) son buenos ejemplos. Este tutorial solo cubrirá el flujo de autenticación, pero debes tomarte la seguridad de tu aplicación lo más en serio posible.

## Construyendo tu aplicación Gatsby

Comienza creando un nuevo proyecto de Gatsby utilizando el generador `hello-world`:

```shell
gatsby new gatsby-auth gatsbyjs/gatsby-starter-hello-world
cd gatsby-auth
```

Crea un nuevo componente para contener los enlaces. Por ahora, dejaremos el texto que indica que el usuario no ha iniciado sesión; más tarde lo cambiaremos:

```jsx:title=src/components/nav-bar.js
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
    <span>No estás autenticado</span>

    <nav>
      <Link to="/">Inicio</Link>
      {` `}
      <Link to="/">Perfil</Link>
      {` `}
      <Link to="/">Salir</Link>
    </nav>
  </div>
)
```

Y crea el componente de layout que envolverá todas las páginas y mostrará la barra de navegación:

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

Por último, cambia la página de inicio para usar el componente de layout:

```jsx:title=src/pages/index.js
import React from "react"

import Layout from "../components/layout" // highlight-line

// highlight-start
export default () => (
  <Layout>
    <h1>Hola mundo!</h1>
  </Layout>
)
// highlight-end
```

## Servicio de autenticación

Para este tutorial, utilizarás un usuario y una contraseña hardcodeados. Crea la carpeta `src/services` y añade el siguiente contenido al archivo `auth.js`:

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

## Creando rutas únicas del cliente

Al comienzo de este tutorial, creaste un sitio Gatsby de "hola mundo", que incluía la librería `@reach/router`. Ahora, utilizando la librería [@reach/router](https://reach.tech/router/), puedes crear rutas disponibles solo para los usuarios registrados. Gatsby utiliza esta biblioteca internamente, por lo que ni siquiera tienes que instalarla.

Primero, crea un archivo `gatsby-node.js` en el directorio raíz de tu proyecto. Define que cualquier ruta que comience por `/app/` es parte del contenido restringido y la página se creará dinámicamente:

```javascript:title=gatsby-node.js
// Implementa el API de Gatsby "onCreatePage" esto es
// llamado después de que cada página es creada
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage } = actions

  // page.matchPath es una key especial que es usada para asociar páginas
  // únicas del cliente.
  if (page.path.match(/^\/app/)) {
    page.matchPath = "/app/*"

    // Actualiza la página
    createPage(page)
  }
}
```

> Nota: Hay un plugin que hace esto mismo: [gatsby-plugin-create-client-paths](/packages/gatsby-plugin-create-client-paths)

Ahora, debes crear una página genérica que se encargará de generar el contenido restringido:

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

Ahora, añade los componentes correspondientes a las nuevas rutas. El componente de perfil para mostrar los datos del usuario:

```jsx:title=src/components/profile.js
import React from "react"

const Profile = () => (
  <>
    <h1>Tu perfil</h1>
    <ul>
      <li>Nombre: Tu nombre aparecerá aqui</li>
      <li>E-mail: Y aqui va tu email</li>
    </ul>
  </>
)

export default Profile
```

El componente de iniciar sesión va a manejar - como ya adivinaste - el proceso de inicio de sesión:

```jsx:title=src/components/login.js
import React from "react"
import { navigate } from "gatsby"
import { handleLogin, isLoggedIn } from "../services/auth"

class Login extends React.Component {
  state = {
    username: ``,
    password: ``,
  }

  handleUpdate = event => {
    this.setState({
      [event.target.name]: event.target.value,
    })
  }

  handleSubmit = event => {
    event.preventDefault()
    handleLogin(this.state)
  }

  render() {
    if (isLoggedIn()) {
      navigate(`/app/profile`)
    }

    return (
      <>
        <h1>Iniciar sesión</h1>
        <form
          method="post"
          onSubmit={event => {
            this.handleSubmit(event)
            navigate(`/app/profile`)
          }}
        >
          <label>
            Nombre de usuario
            <input type="text" name="username" onChange={this.handleUpdate} />
          </label>
          <label>
            Contraseña
            <input
              type="password"
              name="password"
              onChange={this.handleUpdate}
            />
          </label>
          <input type="submit" value="Iniciar sesión" />
        </form>
      </>
    )
  }
}

export default Login
```

Aunque las rutas ahora funcionan, todavía puedes acceder a ellas sin restricción.

## Controlando las rutas privadas

Para comprobar si un usuario puede acceder al contenido, puedes envolver el contenido restringido con un componente `PrivateRoute`:

```jsx:title=src/components/privateRoute.js
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

Ahora puedes editar tu Router para utilizar el componente `PrivateRoute`:

```jsx:title=src/pages/app.js
import React from "react"
import { Router } from "@reach/router"
import Layout from "../components/layout"
import PrivateRoute from "../components/privateRoute" // highlight-line
import Profile from "../components/profile"
import Login from "../components/login"

const App = () => (
  <Layout>
    <Router>
      {/* highlight-next-line */}
      <PrivateRoute path="/app/profile" component={Profile} />
      <Login path="/app/login" />
    </Router>
  </Layout>
)

export default App
```

## Refactorizando para utilizar las nuevas rutas y datos de usuario

Con las rutas únicas del cliente configuradas, ahora debes refactorizar algunos archivos para incorporar los datos del usuario disponibles.

La barra de navegación mostrará el nombre de usuario y la opción de cerrar sesión a los usuarios registrados:

```jsx:title=src/components/nav-bar.js
import React from "react"
import { Link, navigate } from "gatsby" // highlight-line
import { getUser, isLoggedIn, logout } from "../services/auth" // highlight-line

// highlight-start
export default () => {
  const content = { message: "", login: true }
  if (isLoggedIn()) {
    content.message = `Hola, ${getUser().name}`
  } else {
    content.message = "No has iniciado sesión"
  }
  return (
    // highlight-end
    <div
      style={{
        display: "flex",
        flex: "1",
        justifyContent: "space-between",
        borderBottom: "1px solid #d1c1e0",
      }}
    >
      <span>{content.message}</span> {/* highlight-line */}
      <nav>
        <Link to="/">Inicio</Link>
        {` `}
        <Link to="/app/profile">Perfil</Link> {/* highlight-line */}
        {` `}
        {/* highlight-start */}
        {isLoggedIn() ? (
          <a
            href="/"
            onClick={event => {
              event.preventDefault()
              logout(() => navigate(`/app/login`))
            }}
          >
            Cerrar sesión
          </a>
        ) : null}
        {/* highlight-end */}
      </nav>
    </div>
  )
} // highlight-line
```

La página de inicio sugerirá iniciar sesión o ir al perfil, según corresponda:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import { getUser, isLoggedIn } from "../services/auth" // highlight-line

import Layout from "../components/layout"

export default () => (
  <Layout>
    {/* highlight-start */}
    <h1>Hola {isLoggedIn() ? getUser().name : "mundo"}!</h1>
    <p>
      {isLoggedIn() ? (
        <>
          Iniciaste sesión, así que comprueba tu {" "}
          <Link to="/app/profile">perfil</Link>
        </>
      ) : (
        <>
          Debes <Link to="/app/login">iniciar sesión</Link> para ver el contenido
          restringido
        </>
      )}
    </p>
    {/* highlight-end */}
  </Layout>
)
```

Y el perfil mostrará los datos del usuario:

```jsx:title=src/components/profile.js
import React from "react"
import { getUser } from "../services/auth" // highlight-line

const Profile = () => (
  <>
    <h1>Tu perfil</h1>
    <ul>
      {/* highlight-start */}
      <li>Nombre: {getUser().name}</li>
      <li>E-mail: {getUser().email}</li>
      {/* highlight-end */}
    </ul>
  </>
)

export default Profile
```

¡Ahora deberías tener un flujo completo de autenticación, funcionando con inicio de sesión y áreas restringidas solo para usuarios!

## Lectura complementaria

Sí deseas aprender más sobre cómo utilizar soluciones de autenticación listas para producción, estos enlaces pueden ayudarte:

- [Repositorio de Gatsby con autenticación simple](https://github.com/gatsbyjs/gatsby/tree/master/examples/simple-auth)
- [Una _aplicación_ de Gatsby con email](https://github.com/DSchau/gatsby-mail), que usa la API de React Context para controlar la autenticación
- [La tienda de Gatsby para premios y otros extras](https://github.com/gatsbyjs/store.gatsbyjs.org)
- [Building a blog with Gatsby, React and Webtask.io!](https://auth0.com/blog/building-a-blog-with-gatsby-react-and-webtask/)
- [JAMstack PWA — Let’s Build a Polling App. with Gatsby.js, Firebase, and Styled-components Pt. 2](https://medium.com/@UnicornAgency/jamstack-pwa-lets-build-a-polling-app-with-gatsby-js-firebase-and-styled-components-pt-2-9044534ea6bc)
- [JAMstack Hackathon Starter - Starter de apps Gatsby autenticadas con Netlify Identity](/starters/sw-yx/jamstack-hackathon-starter)
- [Livestream de Learn With Jason: How to use Netlify Identity and Netlify Functions (with Shawn Wang)](https://www.youtube.com/watch?v=vrSoLMmQ46k&feature=youtu.be)
