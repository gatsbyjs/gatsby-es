---
title: Creando un Sitio con Autenticación
---

Con Gatsby, puedes crear áreas restringidas en tu aplicación. Para ello, debes
usar el concepto de [rutas solo para clientes](/docs/building-apps-with-gatsby/#client-only-routes).

Usando la librería [@reach/router](https://reach.tech/router/), que viene
instalada con Gatsby, puedes controlar qué componente será cargado cuando cierta
ruta es llamada, y verificar el estado de autenticación antes de servir
el contenido.

## Prerrequisitos

Debes saber cómo configurar un proyecto Gatsby básico. Si lo necesitas, revisa el
[tutorial principal](/tutorial).

## Establecer el flujo de trabajo de autenticación

Para crear un flujo de trabajo común de autenticación, generalmente puedes seguir estos pasos:

- [Crear rutas exclusivas para clientes](/tutorial/authentication-tutorial/#creating-client-only-routes),
  para decirle a Gatsby qué rutas deberían ser renderizadas bajo demanda
- [Envolver contenido privado en un componente _PrivateRoute_](/tutorial/authentication-tutorial/#controlling-private-routes),
  para verificar si un usuario está autenticado o no, por lo tanto, renderizar el contenido o
  redireccionar a otra página (generalmente, la página de inicio de sesión)

## Ejemplo real: la tienda de Gatsby

La [tienda de Gatsby](https://github.com/gatsbyjs/store.gatsbyjs.org) usa este
enfoque al manejar una ruta privada:

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

## Lecturas adicionales

Si quieres más información sobre áreas autenticadas con Gatsby, esta lista (lista no exhaustiva) podría ayudar:

- [Creando un sitio con autenticación de usuarios](/tutorial/authentication-tutorial), un tutorial avanzado de Gatsby
- [repositorio de Gatsby con ejemplo de autenticación simple](https://github.com/gatsbyjs/gatsby/tree/master/examples/simple-auth)
- [Una _aplicación_ de email en Gatsby](https://github.com/DSchau/gatsby-mail), usando la API _Context_ de React para manejar autenticación
- [La tienda de Gatsby para _swag_ y otros productos](https://github.com/gatsbyjs/store.gatsbyjs.org)
- [Añade Autenticación a tus aplicaciones Gatsby con Auth0](/blog/2019-03-21-add-auth0-to-gatsby-livestream/) (transmisión en directo con Jason Lengstorf)
- [Añade Autenticación a tus aplicaciones Gatsby con Okta](https://www.youtube.com/watch?v=7b1iKuFWVSw&t=9s)
- [Otras publicaciones relacionadas con autenticación en el blog de Gatsby](/blog/tags/authentication/)
