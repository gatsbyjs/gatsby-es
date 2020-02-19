---
title: Creación de un plugin local
---

Si un plugin es únicamente aplicable a tu caso de uso específico, o si estás desarrollando un plugin y requieres de un flujo de trabajo más sencillo, un plugin definido localmente es la manera más apropiada de crear y gestionar el código de tu plugin.

<<<<<<< HEAD
Coloca el código en la carpeta `plugins` en la carpeta raíz de tu proyecto de esta manera:
=======
## Project structure for a local plugin

Place the code in the `plugins` folder in the root of your project like this:
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```
/my-gatsby-site
└── gatsby-config.js
└── /src
└── /plugins
    └── /my-own-plugin
        └── package.json
```

<<<<<<< HEAD
**NOTA:** Aún así necesitas añadir el plugin a tu `gatsby-config.js`. No se detectan automáticamente los plugins locales.

**NOTA:** Para que el plugin sea detectado, el valor del nombre de la carpeta raíz del plugin es el que necesita ser referenciado para poder ser cargado (_no_ el _nombre_ en tu archivo package.json). Para la estructura anterior, por ejemplo, la forma correcta de cargar el plugin es:
=======
The plugin also needs to be added to your `gatsby-config.js`, because there is no auto-detection of plugins. It can be added alongside any other 3rd party Gatsby plugins already included in your config.

For the plugin to be discovered when you run `gatsby develop`, the plugin's root folder name needs to match the name used in the `gatsby-config.js` (_not_ the _name_ it goes by in your `package.json` file). For example, in the above structure, the correct way to load the plugin is:
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-third-party-plugin`,
    `my-own-plugin`, // highlight-line
  ],
}
```

<<<<<<< HEAD
Como en todos los archivos `gatsby-*`, el código no se procesará por Babel. Si
deseas utilizar sintaxis JavaScript que no es soportada por tu versión de Node.js,
podrás colocar los archivos en un subdirectorio `src` y generarlos en la raíz de
la carpeta del plugin.
=======
Then the plugin can begin to hook into Gatsby through [Node](/docs/node-apis/) and [SSR](/docs/ssr-apis/) APIs.

## Developing a local plugin that is outside your project

Your plugin doesn't have to be in your project in order to be tested or worked on. If you'd like to [decouple](/docs/glossary#decoupled) your plugin from your site you can follow one of the methods described below. This is a useful thing to do if you want to publish the plugin as its own package, or test/develop a forked version of a community authored plugin.

### Using `require.resolve` and a filepath

Including a `plugins` folder is not the only way to reference a local plugin. Alternatively, you can include a plugin in your `gatsby-config.js` file by directly referencing its path (relative to the `gatsby-config.js` file) with `require`.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-react-helmet`,
    // highlight-start
    {
      // including a plugin from outside the plugins folder needs the path to it
      resolve: require.resolve(`../path/to/gatsby-local-plugin`),
    },
    // highlight-end
  ],
}
```

### Using `npm link` or `yarn link`

You can use [`npm link`](https://docs.npmjs.com/cli/link.html) or [`yarn link`](https://yarnpkg.com/lang/en/docs/cli/link/) to reference a package from another location on your machine.

By running `npm link ../path/to/my-plugin` in the root of your Gatsby site, your computer will create a symlink to your package.

This is a similar process to setting up yarn workspaces for development with Gatsby themes (which is the recommended approach for developing themes). You can read how to setup a site in this manner in the [Building a Theme guide](/tutorial/building-a-theme/#set-up-yarn-workspaces).

**Note**: See an example of using a local plugin from the plugins folder, with `require.resolve`, and `npm link` in [this example repository](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-multiple-local-plugins).

## Compilation and processing with Babel

Like all `gatsby-*` files, the code is not processed by Babel. If you want
to use JavaScript syntax which isn't supported by your version of Node.js, you
can place the files in a `src` subfolder and build them to the plugin folder
root.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc
