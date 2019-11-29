---
title: Enrutamiento
---

## Creando rutas

Gatsby lo hace fácil mediante programación controlar tus páginas. Las páginas pueden ser creadas de tres maneras.

- En el gatsby-node.js de tu sitio implementando el API.
  [`createPages`](/docs/node-apis/#createPages).
- El núcleo de Gatsby convierte automáticamente los componentes React que se encuentran dentro de `src/pages` en páginas.
- Los Plugins también pueden implementar  `createPages` y crear páginas por ti.

Consulta [Creando y Modificando páginas](/docs/creating-and-modifying-pages) para obtener más detalles.

## Vinculación entre rutas

Puedes usar `gatsby-link` para enlazar estas rutas -- esto te proporcionará transiciones de página casi instantáneas mediante _prefetching_. [Más información sobre Gatsby Link
](/docs/gatsby-link/).

También puedes usar enlaces estándar `<a>`, pero en estos casos no obtendrás el beneficio de _prefetching_.

## Crear enlaces con autenticación activada

Si no deseas que todo tu contenido esté disponible públicamente, Gatsby permite crear [rutas "solo para clientes"](/docs/client-only-routes-and-user-authentication), que son accesible tras la autenticación.

<GuideList slug={props.slug} />
