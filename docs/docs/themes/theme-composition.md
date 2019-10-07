---
El titulo: Composición de Temas
---

Al crear temas, muchas veces vale la pena considerar cómo nuestro tema será compuesto con otros. 
En algunos casos, quizás quieras separar su tema en partes más modulares, como `gatsby-theme-blog`
y `gatsby-theme-ecommerce`.

Como los temas aún son tempranos, recomendamos comenzar por construir temas que sean más
monolítico. Es menos alto para empezar y un tema siempre se puede dividir en más pequeños
temas más tarde.

## Diseños

En los temas de Gatsby puede aplicar diseños globales mediante ['wrapRootElement'](/docs/browser-apis/#wrapRootElement)
o [`wrapPageElement`](/docs/browser-apis/#wrapPageElement). Para permitir un mejor tema
composición se recomienda utilizar esta función con moderación. Es muy apropiado para configurar cualquier
los proveedores necesarios de[React Context](https://reactjs.org/docs/context.html). No deberías
agregar cualquier componente de diseño, como encabezados o pies de página, porque se aplicará globalmente que
podría causar problemas con otros temas.

[Leer más sobre diseños y temas gatsby](https://www.christopherbiscardi.com/post/layouts-in-gatsby-themes)
