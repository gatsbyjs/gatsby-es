---
title: Creación de un plugin local
---

Si un plugin es únicamente aplicable a tu caso de uso específico, o si estás desarrollando un plugin y requieres de un flujo de trabajo más sencillo, un plugin definido localmente es la manera más apropiada de crear y gestionar el código de tu plugin.

## Estructura de proyecto para un plugin local

Coloca el código en la carpeta `plugins` en la carpeta raíz de tu proyecto de esta manera:

```text
/my-gatsby-site
└── gatsby-config.js
└── /src
└── /plugins
    └── /my-own-plugin
        └── package.json
```

Este plugin aún así necesita añadirse a tu `gatsby-config.js`. porque no hay detección automática de plugins. Puede agregarse junto a cualquier otro plugin de terceros de Gatsby ya incluidos en tu configuración.

Para que el plugin sea detectado cuando ejecutas `gatsby develop`, el valor del nombre de la carpeta raíz del plugin debe coincidir con el nombre usado en el archivo `gatsby-config.js` (_no_ el _nombre_ en tu archivo package.json). Para la estructura anterior, por ejemplo, la forma correcta de cargar el plugin es:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-third-party-plugin`,
    `my-own-plugin`, // highlight-line
  ],
}
```

Entonces el plugin puede empezarse a agregar a Gatsby mediante APIs de [Node](/docs/node-apis/) y [SSR](/docs/ssr-apis/).

## Desarrollando un plugin local que está fuera del proyecto

Tu plugin no necesita estar en tu proyecto para poder ser probado o trabajar en el. Sí te gustaría [desacoplar](/docs/glossary#decoupled) tu plugin de tu sitio, puedes seguir uno de los métodos descritos abajo. Esto es utíl de hacer sí quieres publicar el plugin en su propio paquete, o probar/desarrollar una versión modificada de un plugin escrito por la comunidad.

<<<<<<< HEAD
## Utilizando `require.resolve` como ruta de archivo
=======
To get started developing a plugin outside of your site's root folder, you can quickly generate one using `gatsby new` with the [starter for plugins](https://github.com/gatsbyjs/gatsby/tree/master/starters/gatsby-starter-plugin):

```shell
gatsby new gatsby-plugin-foo https://github.com/gatsbyjs/gatsby-starter-plugin
```

### Using `require.resolve` and a filepath
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

Incluir una carpeta de `plugins` no es la unica forma de referenciar plugins locales. Alternativamente, puedes incluir un plugin en tu archivo `gatsby-config.js` directamente referenciando su ruta relativa al archivo `gatsby-config.js` con `require`.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-react-helmet`,
    // highlight-start
    {
      // incluir un plugin desde fuera de la carpeta de plugins necesita la ruta al plugin
      resolve: require.resolve(`../ruta/a/gatsby-local-plugin`),
    },
    // highlight-end
  ],
}
```

### Usando `npm link` o `yarn link`

Puedes usar [`npm link`](https://docs.npmjs.com/cli/link.html) o [`yarn link`](https://yarnpkg.com/lang/en/docs/cli/link/) para referenciar un paquete desde otro localización en tu maquina.

Ejecutando `npm link ../ruta/a/mi-plugin` en la raíz de tu sitio de Gatsby, tu computadora creará un `symlink` a tu paquete.

**Nota**: Mira el ejemplo de como usar un plugin local desde la carpeta de plugins, con `require.resolve`, y `npm link` en este [repositorio de ejemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-multiple-local-plugins).

## Compilación y procesamiento con Babel

Como en todos los archivos `gatsby-*`, el código no se procesará por Babel. Si
deseas utilizar sintaxis JavaScript que no es soportada por tu versión de Node.js,
podrás colocar los archivos en un subdirectorio `src` y generarlos en la raíz de
la carpeta del plugin.
