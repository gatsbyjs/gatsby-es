---
title: Theme UI
---

[Theme UI][] es una librería para dar estilo a aplicaciones de React con restricciones de diseño configurables por el usuario.
Te permite dar estilo a cualquier componente en tu aplicación con valores tipográficos, de color y de _layout_ definidos en un tema compartido.
Theme UI es usado actualmente en los temas oficiales de Gatsby, 
pero puede ser usado en cualquier sitio Gatsby o aplicación de React.
Incluye la librería CSS-in-JS [Emotion][] junto con utilidades adicionales para dar estilo como [MDX][] y para usar configuraciones y temas mediante [Typography.js][].

## Usando Theme UI en Gatsby

Theme UI incluye el paquete `gatsby-plugin-theme-ui` para que se integre mejor con tu proyecto Gatsby.

Instala los siguientes paquetes para añadir Theme UI.

```shell
npm install theme-ui gatsby-plugin-theme-ui
```

Después de instalar las dependencias, añade lo siguiente a tu `gatsby-config.js`.

```js:title=gatsby-config.js
module.exports = {
  plugins: ["gatsby-plugin-theme-ui"],
}
```

Theme UI usa un objeto de configuración `theme` para proporcionar color, tipografía, _layout_ y otros valores de estilo compartido a través del [Context de React][].
Esto permite a los componentes dentro de tu sitio añadir estilos basados en un conjunto predefinido de valores.

El plugin de Theme UI usa la [API de _component shadowing_][] para añadir el contexto de tu tema a tu sitio.
Crea una carpeta `src/gatsby-plugin-theme-ui` en tu proyecto, y añade un archivo `index.js` para exportar un tema.

```shell
mkdir src/gatsby-plugin-theme-ui
```

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {}
```

## Creando un tema

Añade un objeto `colors` al archivo creado arriba para almacenar la paleta de colores para tu sitio.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#333",
    background: "#fff",
    primary: "#639",
    secondary: "#ff6347",
  },
}
```

Luego añade algunos valores base tipográficos.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#333",
    background: "#fff",
    primary: "#639",
    secondary: "#ff6347",
  },
  // highlight-start
  fonts: {
    body: "system-ui, sans-serif",
    heading: "system-ui, sans-serif",
    monospace: "Menlo, monospace",
  },
  fontWeights: {
    body: 400,
    heading: 700,
    bold: 700,
  },
  lineHeights: {
    body: 1.5,
    heading: 1.125,
  },
  fontSizes: [12, 14, 16, 20, 24, 32, 48, 64, 72],
  // highlight-end
}
```

Después añade valores para su uso en el _margin_ y en el _padding_.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  colors: {
    text: "#333",
    background: "#fff",
    primary: "#639",
    secondary: "#ff6347",
  },
  fonts: {
    body: "system-ui, sans-serif",
    heading: "system-ui, sans-serif",
    monospace: "Menlo, monospace",
  },
  fontWeights: {
    body: 400,
    heading: 700,
    bold: 700,
  },
  lineHeights: {
    body: 1.5,
    heading: 1.125,
  },
  fontSizes: [12, 14, 16, 20, 24, 32, 48, 64, 72],
  // highlight-start
  space: [0, 4, 8, 16, 32, 64, 128, 256, 512],
  // highlight-end
}
```

Siéntete libre de incluir tantos valores adicionales como te gustaría en tu tema.
Lee más sobre crear temas en la [documentación de Theme UI](https://theme-ui.com/theming).

## Añadiento estilos a elementos

Theme UI usa una función personalizada para añadir soporte para la propiedad `sx` de Theme UI en JSX.
Esta función personalizada es habilitada incluyendo un comentario en la parte superior del archivo:

```js
/** @jsx jsx */
import { jsx } from "theme-ui"
```

La [propiedad `sx`][] es usada para dar estilo a elementos referenciando valores que vienen del tema.

[`sx` prop]: https://theme-ui.com/sx-prop

```jsx:title=src/components/header.js
/** @jsx jsx */
import { jsx } from "theme-ui"

export default props => (
  <header
    sx={{
      // esto usa el valor de `theme.space[4]`
      padding: 4,
      // esto usa los valores de `theme.colors`
      color: "background",
      backgroundColor: "primary",
    }}
  >
    {props.children}
  </header>
)
```

## Usando Theme UI en un tema de Gatsby

Cuando usas Theme UI en un tema de Gatsby, es importante entender cómo el paquete `gatsby-plugin-theme-ui` maneja los objetos de tema de multiples temas de Gatsby y sitios en Gatsby.
Si un tema de Gatsby que usa `gatsby-plugin-theme-ui` es instalado en un sitio,
el archivo `src/gatsby-plugin-theme-ui/index.js` correspodiente sobrescribirá los estilos por defecto.
Esto es intencionado para dar control completo a la persona que use el tema.
Si multiples temas son instalados en el mismo sitio, el último que sea definido en el `array` de `plugins` de tu archivo `gatsby-config.js` tomará precedencia.

Para extender una configuración de Theme UI existente de un tema, puede ser importado y unido con algunos otros valores que te gustarían personalizar. 
Lo siguiente es un ejemplo de extender la configuración de `gatsby-theme-blog`.

```js:title=src/gatsby-plugin-theme-ui/index.js
import baseTheme from "gatsby-theme-blog/src/gatsby-plugin-theme-ui"
import merge from "lodash.merge"

// lodash.merge combinará profundamente los valores personalizados con los
// los valores por defecto del tema del blog
export default merge({}, baseTheme, {
  colors: {
    text: "#222",
    primary: "tomato",
  },
})
```

## Dando estilo a contenido MDX

Theme UI incluye una forma de dar estilo a elementos en documentos MDX sin la necesidad de añadir CSS global a tu sitio.
Esto es útil para crear temas de Gatsby que pueden ser instalados junto a otros temas.

En tu configuración de Theme UI, añade un objeto `styles` a los elementos que vayan a ser renderizados desde MDX.

```js:title=src/gatsby-plugin-theme-ui/index.js
export default {
  // valores base del tema...
  styles: {
    // las claves usadas aquí referencian elementos en MDX
    h1: {
      // el objeto de estilo por cada elemento
      // puede referenciar otros valores en el tema
      fontFamily: "heading",
      fontWeight: "heading",
      lineHeight: "heading",
      marginTop: 0,
      marginBottom: 3,
    },
    a: {
      color: "primary",
      ":hover, :focus": {
        color: "secondary",
      },
    },
    // más estilos pueden ser añadidos tanto como necesites
  },
}
```

Con el ejemplo de arriba, cualquier elemento `<h1>` o `<a>`renderizado desde un archivo MDX incluirá los estilos base.

Para aprender más sobre usar Theme UI en tu proyecto, mira la web oficial de [Theme UI][theme ui]

[theme ui]: https://theme-ui.com
[emotion]: /docs/emotion
[mdx]: /docs/mdx
[typography.js]: /docs/typography-js
[react context]: https://reactjs.org/docs/context.html
[component shadowing api]: /docs/themes/api-reference#component-shadowing