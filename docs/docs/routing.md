---
title: Enrutamiento
---

## Creando rutas

Gatsby lo hace fácil mediante programación controlar sus páginas. Las páginas pueden ser creadas de tres maneras.

- En el gatsby-node.js de su sitio implementando el API.
  [`createPages`](/docs/node-apis/#createPages).
- El núcleo de Gatsby convierte automáticamente los componentes React que se encuentran dentro de `src/pages` en páginas.
- Los Plugins también pueden implementar  `createPages` y crear páginas por usted.

Consulte [Creando y Modificando páginas](/docs/creating-and-modifying-pages) para obtener más detalles.

## Vinculación entre rutas

Puede usar `gatsby-link` para enlazar estas rutas -- esto le proporcionará transiciones de página casi instantáneas mediante prefetching. [Más información sobre Gatsby Link
](/docs/gatsby-link/).

También puede usar enlaces estándar `<a>`, pero en estos casos no  obtendrá el beneficio de prefetching.

## Crear enlaces con autenticación activada

Si no desea que todo su contenido esté disponible públicamente, Gatsby le permite crear [rutas "solo para clientes"](/docs/client-only-routes-and-user-authentication), que viven detrás de una puerta de autenticación.

<GuideList slug={props.slug} />
