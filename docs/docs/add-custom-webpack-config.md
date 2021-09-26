---
title: "Añadiendo Configuraciones Personalizadas de webpack"
---

_Antes de crear una configuración de webpack personalizada, comprueba si ya existe un plugin de Gatsby que soporte tu caso de uso en la [sección de plugins](/docs/plugins/). Si aun no existe ninguno y tu caso de uso es general, te animamos encarecidamente a que contribuyas con tu plugin en la Biblioteca de Plugins de Gatsby para que esté disponible para otros (incluyendo a tu futuro yo)._

Para añadir configuraciones de webpack personalizadas, crea (si aun no lo hay) un fichero `gatsby-node.js` en tu directorio raíz. Dentro de ese fichero, exporta una función llamada `onCreateWebpackConfig`.

Cuando Gatsby crea su configuración de webpack, esta función será llamada permitiéndote modificar la configuración por defecto de webpack usando [webpack-merge](https://github.com/survivejs/webpack-merge).

Gatsby realiza múltiples builds de webpack con configuraciones algo diferentes. A cada uno de esos build lo llamamos "escenario". Existen los siguientes escenarios:

1.  develop: cuando se ejecuta el comando `gatsby develop`. Tiene configuración para _hot reloading_ e inyección de CSS en la página.
2.  develop-html: lo mismo que develop pero sin react-hmre en la configuración de babel para renderizar el componente HTML.
3.  build-javascript: build de producción de JavaScript y CSS. Crea paquetes de ruta JS así como fragmentos comunes para JS y CSS.
4.  build-html: build de producción de páginas HTML estáticas

Revisa [webpack.config.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/webpack.config.js) para ver el código fuente.

Hay muchos plugins en el repositorio de Gatsby que usan esta API para ver ejemplos p. ej.: [Sass](/packages/gatsby-plugin-sass/), [TypeScript](/packages/gatsby-plugin-typescript/), [Glamor](/packages/gatsby-plugin-glamor/), ¡y muchos más!

## Ejemplos

Esto es un ejemplo de como añadir una variable global adicional usando `DefinePlugin` y `less-loader`:

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
            // No necesitamos añadir el plugin ExtractText correspondiente 
            // porque gatsby ya lo incluye y se asegura de que solo
            // corra en las fases adecuadas, p.e. no en desarrollo
            loaders.miniCssExtract(),
            loaders.css({ importLoaders: 1 }),
            // el loader de postcss viene con valores por defecto interesantes
            // incluyendo un autoprefixer para los navegadores configurados
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

### Import absolutos

En lugar de escribir `import Header from '../../components/header'` una y otra vez, puedes escribir  `import Header from 'components/header'` con import absolutos:

```js:title=gatsby-node.js
exports.onCreateWebpackConfig = ({ stage, actions }) => {
  actions.setWebpackConfig({
    resolve: {
      modules: [path.resolve(__dirname, "src"), "node_modules"],
    },
  })
}
```

Puedes encontrar más información sobre _resolve_ y otras opciones en la [documentación oficial de Webpack](https://webpack.js.org/concepts/).

### Modificando el loader de babel

Necesitas esto si quieres hacer cosas como transpilar partes de `node_modules`.

```js:title=gatsby-node.js
exports.onCreateWebpackConfig = ({ actions, loaders, getConfig }) => {
  const config = getConfig()

  config.module.rules = [
    // Omite la regla por defecto donde test === '\.jsx?$'
    ...config.module.rules.filter(
      rule => String(rule.test) !== String(/\.jsx?$/)
    ),

    // Lo recrea con un filtro exclude personalizado
    {
      // Llamado sin ningún argumento, `loader.js` devolverá un
      // objeto como éste: 
      // {
      //   options: undefined,
      //   loader: '/ruta/a/node_modules/gatsby/dist/utils/babel-loader.js',
      // }
      // A no ser que estés reemplazando Babel con un transpilador diferente, 
      // probablemente quieres esto para que Gatsby aplique los plugins/presets
      // requeridos por Babel. Esto también combina tu configuración desde
      // `babel.config.js`.
      ...loaders.js(),

      test: /\.jsx?$/,

      // Excluye todos los node_modules en la transpilación, excepto por 'swiper' y 'dom7'
      exclude: modulePath =>
        /node_modules/.test(modulePath) &&
        !/node_modules\/(swiper|dom7)/.test(modulePath),
    },
  ]

  // Esto reemplazará completamente la configuración de webpack con el objeto modificado.
  actions.replaceWebpackConfig(config)
}
```
