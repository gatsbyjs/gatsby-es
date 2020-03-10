---
title: Creando un Sitio con Autenticación
---

Muchos sitios requieren que los usuarios sean autenticados para proteger datos privados.

## Entendiendo la autenticación entre cliente y servidor

En muchos sitios web modernos, el [cliente](/docs/glossary#client-side) -- o [frontend](/docs/glossary#frontend) -- es [desacoplado](/docs/glossary#decoupled) del [backend](/docs/glossary#backend). Este patrón es como las funciones de Gatsby combinan los datos de una serie de fuentes del backend para facilitar construir el frontend.

Para proveer la funcionalidad de autenticación, otro servicio debe ser agregado y conectado a Gatsby. Hay muchas tecnologías _open source_ que pueden proveer esta funcionalidad. Los ejemplos incluyen:

- Una aplicación Node.js usando Passport.js
- Una API de Ruby on Rails con Devise

Otra opción son tecnologías de terceros como:

- Firebase
- Auth0
- AWS Amplify
- Netlify Identity

Estas herramientas siguen un proceso para poder verificar un usuario en el cliente contra el servicio de autenticación. El servicvio retorna un _token_ que el cliente puede usar para acceder a datos protegidos. Este diagrama visualiza el proceso:

![Diagrama de Gatsby usando un servicio de autenticación para obtener datos de un API](./images/basic-auth.png)

1. Primero, una solicitud es realizada desde el sitio de Gatsby (el cliente) a un servicio de autenticación para realizar una acción como registrar a un nuevo usuario o un _login_.
   
2. Sí las credenciales (cómo nombre de usuario y contraseña) suministradas desde el cliente coinciden con un usuario en el servicio de autenticación, retorna un _token_ (como un _token_ web de JSON, abreviado como JWT) para que el usuario tenga una llave que puede usar para probar que es quien dice ser. Los datos del usuario retornados pueden ser almacenados en la aplicación Gatsby pasandolos a componentes mediante un componente _Provider_ con el API de **Context** de React y el [API `wrapRootElement`](/docs/browser-apis/#wrapRootElement) de Gatsby.

3. Con la llave, el cliente puede hacer solucitudes a una fuente de datos externa como un API (el servidor) donde los datos protegidos son almacenados. La llave es única para un usuario en específico y permite que el cliente acceda a sus datos en específico.

4. El servidor retorna los datos de nuevo al cliente que puede usarla para pasarle información a los componentes.

_**Nota**: este es el mismo patrón que otros sitios hechos con React (cómo Create React App) necesitarían seguir._

## Implementando autenticación en un sitio con Gatsby

Hay ciertas cosas que necesitan ser tomadas en cuenta cuando se implementa autenticación en un sitio con Gatsby, por cómo Gatsby construye páginas únicamente y renderiza recursos estáticos con capacidades dinámicas.

### Configurando rutas solo para cliente

Con Gatsby, eres capaz de crear áreas restringidas en tu aplicación usando [rutas solo para cliente](/docs/building-apps-with-gatsby/#client-only-routes).

Gatsby es un poco [diferente a una aplicación de React tradicional](/docs/adding-app-and-website-functionality/#differences-between-gatsby-and-other-react-apps) en cómo sus rutas y páginas son creadas. Porque los archivos estáticois de HTML generados están en un servidor de archivos, no puedes controlar programáticamente el acceso a esos archivos (por ejemplo: un usuario puede adivinar o teclear una URL y navegar directo a la página). Como la vista general de la [sección de Agregar funcionalidad de sitio web y aplicación](/docs/adding-app-and-website-functionality/#client-only-routes) demuestra, las rutas solo de cliente pueden ser creadas para enrutar un usuario entre páginas usando un enrutador basado en React, opuestamente a navegar entre diferentes arcxhivos estáticos de HTML en un servidor.

Tomando ventaja de este enfoque solo en el cliente el enrutado te permite proteger o personalizar tus rutas. Usando la [líbreria `@reach/router`](https://reach.tech/router/), que viene instalada con Gatsby, puedes configurar un enrutador en una página y controlar que componente se carga cuando cierta ruta es llamada, y comprobar la existencia de una variable como el estado de autenticación antes de guardar el contenido.

<!-- prettier-ignore -->
```jsx
<Router>
  {isAuthenticated ? <PrivateRoute /> : <Login />}
</Router>
```

Ejemplo de código más específicos para este patrón son remarcados en la [guía de Rutas solo para cliente & Autenticación de usuario](/docs/client-only-routes-and-user-authentication/#implementing-client-only-routes).

### Evitando que el código acceda a las globales del navegador durante la compilación

Los objetos globales que son accesibles por el navegador como `localStorage` no están disponibles mientras un sitio de Gatsby se esta construyendo, ya que el compilado se ejecuta en un ambiente Node.js.

Sin embargo, algunos servicios de terceros pueden tratar de acceder a `localStorage` u otros objetos de `window` con métodos internos. Para mantener esos fragmentos alejados de romper el compilado, esas llamadas deberían envolverse en chequeos o hooks de `useEffect` para verificar que el código esta siendo ejecutado en un navegador y que sea omitido durante el proceso de compilado:

```javascript
import app from "firebase/app"

...

if (typeof window !== 'undefined') { // highlight-line
  app.initializeApp(config)
} // highlight-line
```

Más información sobre errores relacionados al compilado estan disponibles en la guía sobre hacer [depuración de compilados HTML](/docs/debugging-html-builds/).

## Ejemplo real: la tienda de Gatsby

La [tienda de Gatsby](https://github.com/gatsbyjs/store.gatsbyjs.org) es una aplicación en vivo hecha con Gatsby que implementa autenticación usando Auth0.

[Funciones útiles](https://github.com/gatsbyjs/store.gatsbyjs.org/blob/master/src/utils/auth.js) en el repositorio de la tienda de Gatsby hacen uso de APIs de Auth0 para autenticar a los usuarios con Github, y envuelven APIs de Auth0 para comprobar que [solo cierto código de Auth0 se ejecuta en el navegador](https://github.com/gatsbyjs/store.gatsbyjs.org/blob/master/src/utils/auth.js#L3).

Para poder proteger contenido autenticado con una ruta privada, un `<Router />` es implementado en el componente `<PrivateRoute />` que comprueba sí el usuario está autenticado o lo redirige a `/login`.

```jsx
// import ...
const PrivateRoute = ({ component: Component, ...rest }) => {
  if (
    !isAuthenticated() &&
    isBrowser &&
    window.location.pathname !== `/login`
  ) {
    // Si no has iniciado sesión, redireccionar a la página de inicio.
    navigate(`/app/login`)
    return null
  }

  return (
    <Router>
      <Component {...rest} />
    </Router>
  )
}
```

Este patrón de ruta privada también es cubierto en el [tutorial para hacer un sitio con autenticación](/tutorial/authentication-tutorial/#controlling-private-routes).

## Lecturas adicionales

Si quieres más información sobre áreas autenticadas con Gatsby, esta lista (lista no exhaustiva) podría ayudar:

- [Creando un sitio con autenticación de usuarios](/tutorial/authentication-tutorial), un tutorial avanzado de Gatsby
- [Repositorio de Gatsby con ejemplo de autenticación simple](https://github.com/gatsbyjs/gatsby/tree/master/examples/simple-auth)
- [Versión en vivo del ejemplo de "Autenticación simple"](https://simple-auth.netlify.com/)
- [Una _aplicación_ de email en Gatsby](https://github.com/DSchau/gatsby-mail), usando la API _Context_ de React para manejar autenticación
- [Añade Autenticación a tus aplicaciones Gatsby con Auth0](/blog/2019-03-21-add-auth0-to-gatsby-livestream/) (transmisión en directo con Jason Lengstorf)
- [Añade Autenticación a tus aplicaciones Gatsby con Okta](https://www.youtube.com/watch?v=7b1iKuFWVSw&t=9s)
- [Otras publicaciones relacionadas con autenticación en el blog de Gatsby](/blog/tags/authentication/)
