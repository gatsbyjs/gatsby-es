---
El titulo: Tema Composición
---

Al construir temas, a menudo es que vale la pena de considerar cómo su tema puede formar con otros.
En algunos casos podría querer romper su tema en partes modulares, como `gatsby-theme-blog`
y `gatsby-theme-ecommerce`.

Dado que los temas son todavía temprano, recomendamos empezar por construir temas que son más
Monolíticos. Es menos sobrecarga para empezar y un tema siempre puede ser dividido en pequeños
temas posteriormente.

## El diseño

En temas de Gatsby puede aplicar disposiciones globales usando ['wrapRootElement'](/docs/browser-apis/#wrapRootElement)
o [`wrapPageElement`](/docs/browser-apis/#wrapPageElement). A fin de permitir una mejor tema
La composición se recomienda el uso de esta función con moderación. Es una estupendo opción para configurar cualquier
Es necesario [React Context](https://reactjs.org/docs/context.html) la proveedor. Normalmente no debe
agregar ningún componente de diseño, como encabezados o pies de página, porque se aplicará globalmente, lo que
podría causar problemas con otros temas.

[Leer más sobre diseños y temas gatsby](https://www.christopherbiscardi.com/post/layouts-in-gatsby-themes)
