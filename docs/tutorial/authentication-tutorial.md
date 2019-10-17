---
título: Crear un sitio con autenticación de usuario
---

A veces, debe crear un sitio con contenido cerrado, disponible solo para usuarios autenticados. Con Gatsby, puede lograr esto usando el concepto de [rutas solo para clientes] (/ docs / building-apps-with-gatsby / # Client-only-routes), para definir qué páginas puede ver un usuario solo después de iniciar sesión.

## Prerrequisitos

Ya debería haber configurado su entorno para poder usar el `gatsby-cli`. Un buen punto de partida es el [tutorial principal] (/ tutorial).

## Aviso de seguridad

En producción, debe usar una solución probada y sólida para manejar la autenticación. [Auth0](https://www.auth0.com), [Firebase](https://firebase.google.com) y [Passport.js](http://passportjs.org) son buenos ejemplos. Este tutorial solo cubrirá el flujo de trabajo de autenticación, pero debe tomar la seguridad de su aplicación lo más en serio posible.

## Construyendo tu aplicación Gatsby

Comience creando un nuevo proyecto de Gatsby utilizando el iniciador `hello-world` de barebones:

`` `concha gatsby nuevo gatsby-auth gatsbyjs / gatsby-starter-hello-world cd gatsby-auth `` `

Cree un nuevo componente para contener los enlaces. Por ahora, actuará como marcador de posición:

`` `jsx: title = src / components / nav-bar.js
importar Reaccionar desde "reaccionar"
importar {Link} desde "gatsby"

export default () => (
  <div
    estilo = {{
      pantalla: "flex",
      flex: "1",
      justifyContent: "espacio intermedio",
      borderBottom: "1px solid # d1c1e0",
    }}
  >
    <span> No has iniciado sesión </span>

<nav>
      <Link to = "/"> Inicio </Link>
      {`} <Enlace a = "/"> Perfil </Link> {`}
      <Link to = "/"> Cerrar sesión </Link>
    </nav>
  </div>
)
`` `

Y cree el componente de diseño que envolverá todas las páginas y mostrará la barra de navegación:

`` `jsx: title = src / components / layout.js
importar Reaccionar desde "reaccionar"

importar NavBar desde "./nav-bar"

Diseño const = ({children}) => (
  <>
    <NavBar />
    {niños}
  </>
)

exportar diseño predeterminado
`` `

Por último, cambie la página de índice para usar el componente de diseño:

`` `jsx: title = src / pages / index.js
importar Reaccionar desde "reaccionar"

importar diseño desde "../components/layout" // resaltar línea

// destacado-inicio
export default () => (
  <Diseño>
    <h1> ¡Hola mundo! </h1>
  </Layout>
)
// punto culminante
`` `

## Servicio de autenticación

Para este tutorial, utilizará un usuario / contraseña codificados. Cree la carpeta `src / services` y agregue el siguiente contenido al archivo`auth.js`:

`` `javascript: title = src / services / auth.js
export const isBrowser = () => typeof window! == "undefined"

export const getUser = () =>
  isBrowser () && window.localStorage.getItem ("gatsbyUser")
    ? JSON.parse (window.localStorage.getItem ("gatsbyUser"))
    : {}

const setUser = usuario =>
  window.localStorage.setItem ("gatsbyUser", JSON.stringify (usuario))

export const handleLogin = ({nombre de usuario, contraseña}) => {
  if (nombre de usuario === `juan` && contraseña ===`pasar`) {
    return setUser ({
      nombre de usuario: `john`,
      nombre: `Johnny`,
      correo electrónico: `johnny @ example.org`,
    })
  }

falso retorno
}

export const isLoggedIn = () => {
  usuario const = getUser ()

volver !! user.username
}

export const logout = callback => {
  setUser ({})
  llamar de vuelta()
}
`` `

## Crear rutas solo para clientes

Al comienzo de este tutorial, creó un sitio Gatsby "hello world", que incluye la biblioteca `@ reach / router`. Ahora, utilizando la biblioteca [@ reach / router](https://reach.tech/router/), puede crear rutas disponibles solo para los usuarios registrados. Gatsby utiliza esta biblioteca bajo el capó, por lo que ni siquiera tiene que instalarla.

Primero, cree `gatsby-node.js` en el directorio raíz de su proyecto. Definirá que cualquier ruta que comience con `/ app /` es parte de su contenido restringido y la página se creará a pedido:

`` `javascript: title = gatsby-node.js
// Implemente la API de Gatsby "onCreatePage". Esto es
// se llama después de crear cada página.
exportaciones.onCreatePage = asíncrono ({página, acciones}) => {
  const {createPage} = acciones

// page.matchPath es una clave especial que se utiliza para hacer coincidir páginas
  // solo en el cliente.
  if (page.path.match (/ ^ \ / app /)) {
    page.matchPath = "/ app / \*"

// Actualiza la página.
    createPage (página)
  }
}
`` `

> Nota: Hay un complemento conveniente que ya funciona para usted: [gatsby-plugin-create-client-paths] (/ packages / gatsby-plugin-create-client-paths)

Ahora, debe crear una página genérica que tendrá la tarea de generar el contenido restringido:

`` `jsx: title = src / pages / app.js
importar Reaccionar desde "reaccionar"
importar {Router} desde "@ reach / router"
importar diseño desde "../components/layout"
Importar perfil desde "../components/profile"
importar Iniciar sesión desde "../components/login"

const App = () => (
  <Diseño>
    <Router>
      <Ruta del perfil = "/ aplicación / perfil" />
      <Ruta de acceso = "/ app / login" />
    </Router>
  </Layout>
)

Exportar aplicación predeterminada
`` `

A continuación, agregue los componentes con respecto a esas nuevas rutas. El componente de perfil para mostrar los datos del usuario:

`` `jsx: title = src / components / profile.js
importar Reaccionar desde "reaccionar"

Perfil const = () => (
  <>
    <h1> Tu perfil </h1>
    <ul>
