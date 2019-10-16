---
título: Crear un sitio con autenticación de usuarios
---

A veces, debes crear un sitio con contenido cerrado, disponible solo para usuarios autenticados. Con Gatsby, puedes lograr esto usando el concepto de [rutas únicas del cliente](/docs/building-apps-with-gatsby/#Client-only-routes), para definir qué páginas puede ver un usuario solo después de iniciar sesión.

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

Y crea el componente de maquetación que envolverá todas las páginas y mostrará la barra de navegación:

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

Por último, cambia la página de índice para usar el componente de maquetación:

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

## El servicio de autenticación

Para este tutorial, utilizará un usuario y una contraseña hardcodeados. Crea la carpeta `src/services` y añade el siguiente contenido al archivo `auth.js`:

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
// Implement the Gatsby API “onCreatePage”. This is
// called after every page is created.
exports.onCreatePage = async ({ page, actions }) => {
  const { createPage } = actions

  // page.matchPath is a special key that's used for matching pages
  // only on the client.
  if (page.path.match(/^\/app/)) {
    page.matchPath = "/app/*"

    // Update the page.
    createPage(page)
  }
}
```

> Nota: Hay un plugin que hace esto mismo: [gatsby-plugin-create-client-paths](/packages/gatsby-plugin-create-client-paths)

Ahora, debes crear una página abstracta que se encargará de generar el contenido restringido:

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

A continuación, añade los componentes relacionados con esas nuevas rutas. El componente de perfil para mostrar los datos del usuario:

```jsx:title=src/components/profile.js
import React from "react"

const Profile = () => (
  <>
    <h1>Your profile</h1>
    <ul>
      <li>Name: Your name will appear here</li>
      <li>E-mail: And here goes the mail</li>
    </ul>
  </>
)

export default Profile
```

El componente de login, que se ocuará de - lo has adivinado - el proceso de inicio de sesión:

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
        <h1>Log in</h1>
        <form
          method="post"
          onSubmit={event => {
            this.handleSubmit(event)
            navigate(`/app/profile`)
          }}
        >
          <label>
            Username
            <input type="text" name="username" onChange={this.handleUpdate} />
          </label>
          <label>
            Password
            <input
              type="password"
              name="password"
              onChange={this.handleUpdate}
            />
          </label>
          <input type="submit" value="Log In" />
        </form>
      </>
    )
  }
}

export default Login
```

Aunque las rutas ahora funcionan, todavía puedes acceder a ellas sin restricción.

## Controlando las rutas privadas

Para comprobar si un usuario puede acceder el contenido, puedes envolver el contenido restringido dentro de un componente PrivateRoute:

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

Ahora puedes editar tu Router para usar el componente PrivateRoute:

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

## Refactorizando para usar las nuevas rutas y datos de usuario

Con las rutas únicas del cliente configuradas, debes refactorizar algunos archivos para incorporar los datos del usuario disponibles.

La barra de navegación mostrará el nombre de usuario y la opción de cerrar sesión a usuarios registrados:

```jsx:title=src/components/nav-bar.js
import React from "react"
import { Link, navigate } from "gatsby" // highlight-line
import { getUser, isLoggedIn, logout } from "../services/auth" // highlight-line

// highlight-start
export default () => {
  const content = { message: "", login: true }
  if (isLoggedIn()) {
    content.message = `Hello, ${getUser().name}`
  } else {
    content.message = "You are not logged in"
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
        <Link to="/">Home</Link>
        {` `}
        <Link to="/app/profile">Profile</Link> {/* highlight-line */}
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
            Logout
          </a>
        ) : null}
        {/* highlight-end */}
      </nav>
    </div>
  )
} // highlight-line
```

La página de índice sugerirá hacer login o ir al perfil, según corresponda:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import { getUser, isLoggedIn } from "../services/auth" // highlight-line

import Layout from "../components/layout"

export default () => (
  <Layout>
    {/* highlight-start */}
    <h1>Hello {isLoggedIn() ? getUser().name : "world"}!</h1>
    <p>
      {isLoggedIn() ? (
        <>
          You are logged in, so check your{" "}
          <Link to="/app/profile">profile</Link>
        </>
      ) : (
        <>
          You should <Link to="/app/login">log in</Link> to see restricted
          content
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
    <h1>Your profile</h1>
    <ul>
      {/* highlight-start */}
      <li>Name: {getUser().name}</li>
      <li>E-mail: {getUser().email}</li>
      {/* highlight-end */}
    </ul>
  </>
)

export default Profile
```

¡Ahora deberías tener un flujo de autenticación completo, funcionando con inicio de sesión y área restringida!

## Lectura complementaria

Si quieres aprender mas sobre cómo usar soluciones de autenticación preparadas para producción, los siguientes links pueden ser de utilidad:

- [El ejemplo de autenticación simple del repo de Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/examples/simple-auth)
- [Una _aplicación_ de email con Gatsby](https://github.com/DSchau/gatsby-mail), que usa la API de Contextos de React para controlar la autenticación
- [La tienda de merchandising de Gatsby](https://github.com/gatsbyjs/store.gatsbyjs.org)
- [Building a blog with Gatsby, React and Webtask.io!](https://auth0.com/blog/building-a-blog-with-gatsby-react-and-webtask/)
- [JAMstack PWA — Let’s Build a Polling App. with Gatsby.js, Firebase, and Styled-components Pt. 2](https://medium.com/@UnicornAgency/jamstack-pwa-lets-build-a-polling-app-with-gatsby-js-firebase-and-styled-components-pt-2-9044534ea6bc)
- [JAMstack Hackathon Starter - Un generador de apps Gatsby autenticadas con Netlify Identity](/starters/sw-yx/jamstack-hackathon-starter)
- [Livestream de Learn With Jason: How to use Netlify Identity and Netlify Functions (with Shawn Wang)](https://www.youtube.com/watch?v=vrSoLMmQ46k&feature=youtu.be)
