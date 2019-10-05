---
title: 'Escribiendo documentación con Docz'
---

Escribir buena documentación es importante para los que mantienen tus proyectos (y para ti mismo en el futuro). [Docz](https://www.docz.site) es un estupendo generador de documentación. Te permite escribir documentación interactiva para tus componentes React con muy poco esfuerzo.

Docz aprovecha archivos `mdx` – archivos Markdown con JSX – que convierte **componentes React** a archivos Markdown. Sabiendo tus PropTypes o tipos Flow o los tipos TypeScript, puede generar una **tabla de propiedades** para documentar apropiadamente como usar tus componentes. Adicionalmente, puedes proveer **código editable** de tus componentes, para que cualquiera pueda verlos en acción, modificar el código y ver los cambios en directo, o copiar esa parte del código y usarlo en otro lado.

Si estas empezando tu proyecto Gatsby desde cero y te gustaría tener una excelente documentación, con soporte para Docz, puedes usar [`gatsby-starter-docz`](https://github.com/pedronauck/gatsby-starter-docz). También puedes encontrar mas información al final de esta guía en la sección [otros recursos](#other-resources).

Como alternativa, la siguiente guía debería ayudarte a que utilices Docz en un proyecto Gatsby existente.

## Configurando tu ambiente

Primero, si aún no tienes un proyecto Gatsby configurado, usa la CLI de Gatsby para crear un nuevo sitio:

```shell
gatsby new my-gatsby-site-with-docz
```

Para configurar Docz necesitas instalar el tema Docz de Gatsby, y agregar cierta configuración personalizada. Asegurate de estar en el directorio raíz de tu proyecto Gatsby:

```shell
cd my-gatsby-site-with-docz
```

Instala el paquete `gatsby-theme-docz`:

```shell
npm install --save gatsby-theme-docz@next
```

Agrega `gatsby-theme-docz` bajo `plugins` en `gatsby-config.js`:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    //highlight-next-line
    `gatsby-theme-docz`,
    // Your plugins go here
  ],
};
```

## Escribiendo documentación

Docz busca archivos `mdx` en tus directorios y los renderiza. Crea una carpeta `docs` en la raíz de tu proyecto. Coloca un archivo `index.mdx` dentro del directorio con el siguiente contenido:

```mdx:title=docs/index.mdx
---
name: Getting Started
route: /
---

# Getting Started

## Hello world

Type here the most beautiful getting started that you ever saw!
```

Inicia el servidor de desarrollo con el comando `gatsby develop` y deberías sentirte bienvenido con el diseño por defecto de Docz y una cabecera "Getting Started". Detén el servidor de desarrollo después de verificar que todo funciona.

Condimentemos un poco más agregando y renderizando componentes React. Para mantener las cosas simples puedes crear un componente botón en el mismo directorio `docs`.

```jsx:title=docs/button.jsx
import React from 'react';
import PropTypes from 'prop-types';

const scales = {
  small: {
    fontSize: '16px',
  },
  normal: {
    fontSize: '18px',
  },
  big: {
    fontSize: '22px',
  },
};

export const Button = ({ children, scale }) => (
  <button style={scales[scale]}>{children}</button>
);

Button.propTypes = {
  children: PropTypes.node.isRequired,
  scale: PropTypes.oneOf(['small', 'normal', 'big']),
};

Button.defaultProps = {
  scale: 'normal',
};
```

El botón mostrará su texto por defecto con la propiedad `font-size` a `18px`, aunque puedes especificar el tamaño `small` & `big`. Estas propiedades serán mostradas posteriormente por Docz.

> **Nota:** Si tu componente depende de `StaticQuery` o `graphql`, considera separarlo en dos componentes más pequeños:
>
> - un componente React encargado solo de la **capa UI**, y
> - otro encargándose de la **capa de datos**.
>
> Podrías exhibir el componente React encargado de la capa UI en tu archivo `mdx` y el componente encargado de los datos podría usarlo para renderizar los datos obtenidos gracias a `StaticQuery` y `graphql`.

Crea un nuevo archivo en el directorio `docs` para documentar el componente botón recién creado. Nombra el archivo `button.mdx`:

```mdx:title=docs/button.mdx
---
name: Button
menu: Components
---

# Button

Buttons make common actions more obvious and help users more easily perform them. Buttons use labels and sometimes icons to communicate the action that will occur when the user touches them.
```

Docz ofrece algunos componentes internos que puedes usar para mostrar el componente y sus propiedades. Importa ambos (Playground y Props) y también tu propio componente en el documento para usarlos:

```mdx:title=docs/button.mdx
---
name: Button
menu: Components
---

// highlight-start
import { Playground, Props } from "docz"
import { Button } from "./button"
// highlight-end

# Button

Buttons make common actions more obvious and help users more easily perform them. Buttons use labels and sometimes icons to communicate the action that will occur when the user touches them.

// highlight-start

## Properties

<Props of={Button} />

## Basic usage

<Playground>
  <Button>Click me</Button>
</Playground>

## With different sizes

<Playground>
  <Button scale="small">Click me</Button>
  <Button scale="normal">Click me</Button>
  <Button scale="big">Click me</Button>
</Playground>
// highlight-end
```

Inicia el servidor de desarrollo nuevamente y deberías ver las propiedades (children y scale), un editor de código mostrando el botón normal, y un editor de código mostrando el botón en sus tres tamaños.

## Configuración

Normalmente puedes establecer tu configuración usando el archivo `doczrc.js` ([mira todas las opciones disponibles](https://www.docz.site/docs/project-configuration)) o si quieres establecer algunas opciones por defecto en tu tema, puedes establecer `options` (opciones) en la definición del tema.

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    //highlight-start
    {
      resolve: `gatsby-theme-docz`,
      options: {
        // Your options here
      },
    },
    //hightlight-end
    // Your plugins go here
  ],
};
```

> ¡Recomendamos encarecidamente que establezcas tu configuración usando `doczrc.js`! Live reloading (actualización automática de tu sitio) solo funcionará con el archivo de configuración y no con las configuraciones dentro de la definición del tema.

## Otros recursos

- Para más información de Docz visita [el sitio de Docz](https://docz.site/) y en particular la [documentación de Gatsby theme](https://www.docz.site/docs/gatsby-theme)
- Revisa el [Docz starter](https://github.com/pedronauck/gatsby-starter-docz) oficial.
