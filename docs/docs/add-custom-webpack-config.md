---
title: "Agregar una configuración de paquete web personalizado"
---

_Antes de crear la configuración personalizada del paquete web, compruebe si hay un Gatsby
ya construido que maneja su caso de uso en el
[plugins section](/docs/plugins/). Si aún no hay uno y su caso de uso es un
general, le animamos a contribuir de nuevo su plugin a la
Gatsby Plugin Library para que esté disponible para otros (incluyendo su futuro yo 😀). _

Para agregar configuraciones personalizadas de webpack, cree (si aún no hay una) un
`gatsby-node.js` en su archivo root directorio. Dentro de este archivo, exporte un
función llamada `onCreateWebpackConfig`.

Cuando Gatsby crea su configuración de paquete web, esta función se llamará permitiendo
para modificar la configuración predeterminada del paquete web usando
[webpack-merge](https://github.com/survivejs/webpack-merge).

Gatsby hace varias compilaciones de webpack con una configuración algo diferente. Nosotros
llame a cada tipo de compilación a una «etapa». Existen las siguientes etapas:

1.  develop: al ejecutar el comando `gatsby develop`. Tiene configuración para caliente
 recarga e inyección de CSS en la página

2. develop-html: lo mismo que desarrollar pero sin react-hmre en la configuración de babel para
 renderizando el componente HTML.

3. build-javascript: JavaScript de producción y compilación CSS. Crea paquetes JS de ruta también
 como fragmentos comunes para JS y CSS.

4. build-html: creación de producción páginas HTML estáticas

Comprobar
[webpack.config.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/webpack.config.js)
para la fuente.

Hay muchos complementos en el repositorio de Gatsby usando esta API para buscar ejemplos
e.g. [Sass](/packages/gatsby-plugin-sass/),
[TypeScript](/packages/gatsby-plugin-typescript/),
[Glamor](/packages/gatsby-plugin-glamor/), y muchos más!

## Ejemplos

Aquí hay un ejemplo que agrega una variable global adicional a través de la `DefinePlugin` y el `less-loader`:

```js:title=gatsby-node.js
exports.onCreateWebpackConfig = ({
  stage,
  rules,
  loaders,
  plugins,
  actions,
}) => {
  actions.setWebpackConfig({
    module: {
      rules: [
        {
          test: /\.less$/,
          use: [
            // We don't need to add the matching ExtractText plugin
            // because gatsby already includes it and makes sure its only
            // run at the appropriate stages, e.g. not in development
            loaders.miniCssExtract(),
            loaders.css({ importLoaders: 1 }),
            // the postcss loader comes with some nice defaults
            // including autoprefixer for our configured browsers
            loaders.postcss(),
            `less-loader`,
          ],
        },
      ],
    },
    plugins: [
      plugins.define({
        __DEVELOPMENT__: stage === `develop` || stage === `develop-html`,
      }),
    ],
  })
}
```

### Importaciones absolutas

En lugar de escribir `import Header from '../../components/header'` una y otra vez puedes escribir `import Header from 'components/header'` con importaciones absolutas:

```js:title=gatsby-node.js
exports.onCreateWebpackConfig = ({ stage, actions }) => {
  actions.setWebpackConfig({
    resolve: {
      modules: [path.resolve(__dirname, "src"), "node_modules"],
    },
  })
}
```

Siempre puedes encontrar más información sobre _resolve_ y otras opciones en el [Webpack docs](https://webpack.js.org/concepts/).

### Modificación del cargador babel

Necesita esto si desea hacer cosas como transponer partes de `node_modules`.

```js:title=gatsby-node.js
exports.onCreateWebpackConfig = ({ actions, loaders, getConfig }) => {
  const config = getConfig()

  config.module.rules = [
    // Omit the default rule where test === '\.jsx?$'
    ...config.module.rules.filter(
      rule => String(rule.test) !== String(/\.jsx?$/)
    ),

    // Recreate it with custom exclude filter
    {
      // Called without any arguments, `loaders.js` will return an
      // object like:
      // {
      //   options: undefined,
      //   loader: '/path/to/node_modules/gatsby/dist/utils/babel-loader.js',
      // }
      // Unless you're replacing Babel with a different transpiler, you probably
      // want this so that Gatsby will apply its required Babel
      // presets/plugins.  This will also merge in your configuration from
      // `babel.config.js`.
      ...loaders.js(),

      test: /\.jsx?$/,

      // Exclude all node_modules from transpilation, except for 'swiper' and 'dom7'
      exclude: modulePath =>
        /node_modules/.test(modulePath) &&
        !/node_modules\/(swiper|dom7)/.test(modulePath),
    },
  ]

  // Esto reemplazará completamente la configuración del paquete web con el objeto modificado.
  actions.replaceWebpackConfig(config)
}
```
