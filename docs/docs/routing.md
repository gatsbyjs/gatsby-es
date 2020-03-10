---
title: Enrutamiento
---

Parte de lo que hace a los sitios de Gatsby tan rápidos es que una gran cantidad del trabajo es realizado en tiempo de compilación y el tiempo de ejecución del sitio solo usa mayormente [contenido estático](/docs/adding-app-and-website-functionality/#static-pages). Durante este proceso, Gatsby crea rutas para acceder a ese contenido, manejando el [enrutado](/docs/glossary#routing) por ti. Navegar en una aplicación de Gatsby requiere entendimiento de que son esas rutas y cómo son generadas.

Alternativamente, tu aplicación puede incluir funcionalidades que no pueden ser manejadas en tiempo de compilación o mediante [re-hidratación](/docs/adding-app-and-website-functionality/#how-hydration-makes-apps-possible). Esto incluye cosas como autenticación u obtener contenido dinámico. Para manejar esas páginas, puedes hacer uso de [rutas solo para cliente](/docs/client-only-routes-and-user-authentication) utilizando [`@reach/router`](/docs/reach-router-and-gatsby/) que está incluido en Gatsby.

## Creando rutas

Gatsby lo hace fácil mediante programación controlar tus páginas. Las páginas pueden ser creadas de tres maneras.

- En el gatsby-node.js de tu sitio implementando el API.
  [`createPages`](/docs/node-apis/#createPages).
- El núcleo de Gatsby convierte automáticamente los componentes React que se encuentran dentro de `src/pages` en páginas.
- Los Plugins también pueden implementar  `createPages` y crear páginas por ti.

Consulta [Creando y Modificando páginas](/docs/creating-and-modifying-pages) para obtener más detalles.

Cuando Gatsby crea páginas, automáticamente genera rutas para acceder a ellas. Esto es diferente dependiendo de como fue definida la página.

### Páginas definidas en `src/pages`

Cada archivo `.js` dentro de `src/pages` generará su propia página en tu sitio de Gatsby. La ruta a esas páginas corresponde a la estructura de archivos donde se encuentra.

Por ejemplo, `contact.js` será encontrado en `yoursite.com/contact`. Y `home.js` será encontrado en `yoursite.com/home`. Esto funciona en cualquier nivel en el que el archivo esté creado. Sí `contact.js` es movido a un directorio llamado `information`, ubicado en `src/pages`, la página ahora será encontrada en `yoursite.com/information/contact`.

La excepción a esta regla es cualquier archivo llamado `index.js`. Archivos con este nombre son marcados como la raíz del directorio en el que se encuentran. Esto significa que el `index.js` en la raíz del directorio `src/pages` es accedido mediante `yoursite.com`. Sin embargo, sí hay un `index.js` dentro del directorio `information`, es encontrado en `yoursite.com/information`.

Ten en cuenta que sí no hay ningún archivo `index.js` en un directorio en particular, esa página raíz no existe, y los intentos de navegar a ella te redigirán a una [página 404](/docs/add-404-page/). Por ejemplo, `yoursite.com/information/contact` puede existir, pero eso no garantiza que `yoursite.com/information` exista.

### Páginas creadas con la acción `createPage`

Otra forma de crear páginas es en tu archivo `gatsby-node.js` usando la acción `createPage`, una función de Javascript. Cuando las páginas son definidas de esta forma, la ruta es configurada explícitamente. Por ejemplo:

```js:title=gatsby-node.js
createPage({
  path: "/routing",
  component: routing,
  context: {},
})
```

Para más información sobre esta acción, visita la [documentación del API `createPage`](/docs/actions/#createPage).

## Rutas en conflicto

Ya que hay multiples formas de crear una página, diferentes plugins, temas, o secciones de código en tu archivo `gatsby-node` puede que accidentalmente creen multiples páginas que se supone deben acceder por la misma ruta. CUando esto ocurre, Gatsby mostrará una advertencia en tiempo de compilación, pero el sitio se compilará exitosamente. En esta situación, la página que se construyó de último será accesible y cualquier otra página en conflicto no lo será. Cambiar cualquier ruta en conflicto para producir URLs únicas debería acabar con el problema.

## Rutas anidadas

Sí tu meta es definir rutas que están a varios niveles de profundidad, cómo `/portfolio/art/item1`, puede ser realizado directamente cuando se crean las páginas como se menciona en [Creando rutas](#creating-routes).

Alternativamente, sí quieres crear páginas que mostrarán diferentes sub-componentes dependiendo de la URl de la ruta (cómo un widget específico de barra lateral), Gatsby puede encargarse de esto al nivel de la página usando [layouts](/docs/layout-components/).

## Enlazado entre rutas

Para poder enlazar páginas, puedes usar [`gatsby-link`](/docs/gatsby-link/). Usar `gatsby-link` te da [beneficios de rendimiento](#performance-and-prefetching).

Alternativamente, puede navegar entre páginas usando etiquetas `<a>` por defecto, pero no obtendrás el beneficio de _prefetching_ (pre-cargar).

## Crear enlaces con autenticación activada

Para páginas tratando con información delicada, u otro comportamiento dinámico, puede que quieras manejar esta información en el lado del servidor. Gatsby te permite crear [rutas solo para el cliente](/docs/client-only-routes-and-user-authentication) que viven más allá de la autenticación, asegurando que la información está disponible solo para usuarios autorizados.

## Rendimiento y Prefetching (Pre-carga)

Para mejorar el rendimiento, Gatsby mira los enlaces que aparecen en la página actual para realizar `prefetching` (pre-carga). Antes de que el usuario siquiera haya hecho click en un enlace, Gatsby ya ha empezado a obtener la página a la que apunta el enlace. [Aprende más sobre prefetching](/docs/how-code-splitting-works/#prefetching-chunks).

<GuideList slug={props.slug} />
