---
título: "Agregar una configuración de paquete web personalizado"
---

_Antes de crear una configuración de paquete web personalizada, verifique si hay un Gatsby
plugin ya construido que maneja su caso de uso en el
[sección de complementos] (/ docs / plugins /). Si aún no hay uno y su caso de uso es un
en general, le recomendamos encarecidamente que contribuya de nuevo su complemento a la
Gatsby Plugin Library para que esté disponible para otros (incluido tu futuro yo 😀) ._

Para agregar configuraciones de paquete web personalizadas, cree (si aún no hay una) un
Archivo `gatsby-node.js` en su directorio raíz. Dentro de este archivo, exporta un
función llamada `onCreateWebpackConfig`.

Cuando Gatsby crea su configuración de paquete web, esta función se llamará permitiendo
puede modificar la configuración predeterminada del paquete web usando
[combinación de paquetes web] (https://github.com/survivejs/webpack-merge).

Gatsby realiza múltiples compilaciones de paquetes web con una configuración algo diferente. Nosotros
llame a cada tipo de construcción una "etapa". Existen las siguientes etapas:

1. desarrollo: al ejecutar el comando `gatsby desarrollo`. Tiene configuración para caliente
    recarga e inyección CSS en la página
2. development-html: igual que desarrollo pero sin react-hmre en la configuración de babel para
    renderizando el componente HTML.
3. build-javascript: producción de JavaScript y CSS build. Crea paquetes de ruta JS también
    como fragmentos comunes para JS y CSS.
4. build-html: páginas HTML estáticas de construcción de producción

Cheque
[webpack.config.js] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/webpack.config.js)
para la fuente

Hay muchos complementos en el repositorio de Gatsby que usan esta API para buscar ejemplos
p.ej. [Sass] (/ packages / gatsby-plugin-sass /),
[TypeScript] (/ packages / gatsby-plugin-typescript /),
[Glamour] (/ packages / gatsby-plugin-glamour /), ¡y muchos más!

## Ejemplos

Aquí hay un ejemplo que agrega una variable global adicional a través del `DefinePlugin` y el` less-loader`:

`` `js: title = gatsby-node.js
exportaciones.onCreateWebpackConfig = ({
  escenario,
  reglas,
  cargadores,
  complementos,
  comportamiento,
}) => {actions.setWebpackConfig ({
    módulo: {
      reglas: [
        {
          prueba: /\.less$/,
          utilizar: [
            // No necesitamos agregar el complemento ExtractText correspondiente
            // porque gatsby ya lo incluye y se asegura de que solo
            // ejecutar en las etapas apropiadas, p. ej. no en desarrollo
            loaders.miniCssExtract (),
            loaders.css ({importLoaders: 1}),
            // el cargador postcss viene con algunos buenos valores predeterminados
            // incluido el corrector automático para nuestros navegadores configurados
            loaders.postcss (),
            «menos cargador»,
          ],
        },
      ],
    },
    complementos: [
      plugins.define ({
        __DEVELOPMENT__: stage === `desarrollo` || etapa === `desarrollo-html`,
      }),
    ],
  })
}
`` `

### Importaciones absolutas

En lugar de escribir `import Header from '../../ components / header'` una y otra vez, simplemente puede escribir` import Header from' components / header'` con importaciones absolutas:

`` `js: title = gatsby-node.js
exportaciones.onCreateWebpackConfig = ({etapa, acciones}) => {
  actions.setWebpackConfig ({
    resolver: {
      módulos: [path.resolve (__ dirname, "src"), "node_modules"],
    },
  })
}
`` `

Siempre puede encontrar más información sobre _resolve_ y otras opciones en el [Webpack docs] oficial (https://webpack.js.org/concepts/).
### Modificando el cargador de babel

Necesita esto si desea hacer cosas como transpilar partes de `node_modules`.

`` `js: title = gatsby-node.js
exportaciones.onCreateWebpackConfig = ({acciones, cargadores, getConfig}) => {
  const config = getConfig ()

  config.module.rules = [
    // Omitir la regla predeterminada donde test === '\ .jsx? $'
    ... config.module.rules.filter (
      rule => String (rule.test)! == String (/ \. jsx? $ /)
    ),

    // Recrea con filtro de exclusión personalizado
    {
      // Llamado sin ningún argumento, `loaders.js` devolverá un
      // objeto como:
      // {
      // opciones: indefinido,
      // cargador: '/path/to/node_modules/gatsby/dist/utils/babel-loader.js',
      //}
      // A menos que estés reemplazando a Babel con un transpilador diferente, probablemente
      // quiero esto para que Gatsby aplique su Babel requerido
      // presets / plugins. Esto también se fusionará en su configuración de
      // `babel.config.js`.
      ... loaders.js (),

      prueba: /\.jsx?$/,

      // Excluir todos los node_modules de la transpilación, excepto 'swiper' y 'dom7'
      excluir: modulePath =>
        /node_modules/.test(modulePath) &&
        ! / node_modules \ / (swiper | dom7) /. test (modulePath),
    },
  ]

  // Esto reemplazará completamente la configuración del paquete web con el objeto modificado.
  actions.replaceWebpackConfig (config)
}
`` `