---
title: Pruebas visuales con Storybook
---

Saber que tus componentes se ven como deberían en cada permutación no es sólo una gran manera de probarlos visualmente, sino que también provee una "documentación viva" para ellos. Esto facilita a los equipos a:

1. saber qué componentes están disponibles para ellos en un proyecto dado y
2. saber qué propiedades aceptan esos componentes y cuáles son todos los estados de ese componente.

A medida que tu proyecto crece en el tiempo, tener esta información disponible será invaluable. Ésta es la función de la librería [Storybook](https://storybook.js.org/). Storybook es un ambiente de desarrollo de UI para tus componentes UI. Con él, puedes visualizar diferentes estados de tus componentes UI y desarrollarlos interactivamente.

## Configurando tu ambiente

> Ten en cuenta que las instrucciones a continuación están usando [npx](https://www.npmjs.com/package/npx). `npx` es una parte de npm y en este caso te permite generar automáticamente una estructura de archivos/carpetas completa con la configuración por defecto. Si estás ejecutando una versión vieja de `npm` (`<5.2.0`) deberías ejecutar el siguiente comando en su lugar `npm install -g @storybook/cli`. Entonces podrías ejecutar `sb init` desde la raíz del directorio de Gatsby para inicializar Storybook.

Para configurar Storybook necesitas instalar dependencias y algunas configuraciones personalizadas. Puedes empezar rápidamente utilizando el comando automatizado de la línea de comandos desde la raíz de tu proyecto Gatsby:

```shell
npx -p @storybook/cli sb init
```

Este comando agrega una serie de archivos `boilerplate` para Storybook en tu proyecto. Sin embargo, ya que esto es para un proyecto de Gatsby, necesitas actualizar la configuración predeterminada de Storybook un poco para no obtener errores cuando trates de utilizar componentes específicos dentro de las historias.

Para actualizar tu configuración de Storybook abre `.storybook/config.js` y modifica el contenido del siguiente modo:

```js:title=.storybook/config.js
import { configure } from "@storybook/react"
import { action } from "@storybook/addon-actions"

// automáticamente importa todos los archivos terminados en *.stories.js
// highlight-next-line
const req = require.context("../src", true, /.stories.js$/)
function loadStories() {
  req.keys().forEach(filename => req(filename))
}

// highlight-start
// La sobreescritura de Link de Gatsby:
// Gatsby define una llamada global ___loader para prevenir que sus llamadas de métodos creen errores de consola. Debes pisarlo aquí
global.___loader = {
  enqueue: () => {},
  hovering: () => {},
}

// "Mock" interno de Gatsby para evitar errores innecesarios en ambientes de testing de storybook
global.__PATH_PREFIX__ = ""

// Esto es utilizado para sobreescribir el método window.___navigate que Gatsby usa y define para reportar qué camino un Link estaría llevándonos si no estuviese dentro de un storybook
window.___navigate = pathname => {
  action("NavigateTo:")(pathname)
}

configure(loadStories, module)
// highlight-end
```

> Puedes eliminar la carpeta  `stories` de la raíz de tu proyecto o moverla adentro de tu carpeta `src`

Después haz algunos ajustes a la configuración predeterminada de `webpack` para Storybook asi puedes transpilar archivos fuente de Gatsby, y para asegurar que tienes los plugins necesarios de `babel` para transpilar componentes de Gatsby.

Crea un nuevo archivo llamado `webpack.config.js` en la carpeta `.storybook` creada por el CLI de Storybook. Luego ubica el siguiente código en ese archivo (dependiendo en qué versión de Storybook estás utilizando).

**Para Storybook v5:**

```js:title=.storybook/webpack.config.js
module.exports = ({ config }) => {
  // Transpila el módulo de Gatsby porque Gatsby incluye código de ES6 no-transpilado.
  config.module.rules[0].exclude = [/node_modules\/(?!(gatsby)\/)/]

  // Usa el babel-loader instalado que es v8.0-beta (que debe trabajar junto a @babel/core@7)
  config.module.rules[0].use[0].loader = require.resolve("babel-loader")

  // usa @babel/preset-react para JSX y env (en vez de etapas preseteadas)
  config.module.rules[0].use[0].options.presets = [
    require.resolve("@babel/preset-react"),
    require.resolve("@babel/preset-env"),
  ]

  config.module.rules[0].use[0].options.plugins = [
    // use @babel/plugin-proposal-class-properties for class arrow functions
    require.resolve("@babel/plugin-proposal-class-properties"),
    // use babel-plugin-remove-graphql-queries to remove static queries from components when rendering in storybook
    require.resolve("babel-plugin-remove-graphql-queries"),
  ]

  // Prefiere el entrypoint ES6 de Gatsby ES6 sobre el entrypoint de commonjs (principal)
  config.resolve.mainFields = ["browser", "module", "main"]

  return config
}
```

> Nota que si estás utilizando un [StaticQuery](/docs/static-query/) en tus componentes, `babel-plugin-remove-graphql-queries` es necesario para renderizarlos en Storybook. Esto es porque los queries son construídos a la hora del compilado de Gatsby, y no será ejecutado cuando se rendericen los componentes directamente.

> Cuando utilizas TypeScript, agrega esta regla::

```diff:title=.storybook/webpack.config.js
// Prefiere el punto de entrada de ES6 de Gatsby (módulo) sobre el punto de entrada (principal) de commonjs

config.resolve.mainFields = ["browser", "module", "main"]
+
+   config.module.rules.push({
+     test: /\.(ts|tsx)$/,
+     loader: require.resolve('babel-loader'),
+     options: {
+       presets: [['react-app', {flow: false, typescript: true}]],
+       plugins: [
+         require.resolve('@babel/plugin-proposal-class-properties'),
+         // Usa babel-plugin-remove-graphql-queries para eliminar queries estáticas de componentes cuando se renderiza en storybook
+         require.resolve('babel-plugin-remove-graphql-queries'),
+       ],
+     },
+   });
+
+   config.resolve.extensions.push('.ts', '.tsx');
+
return config
```

**Para Storybook v4:**

```js:title=.storybook/webpack.config.js
module.exports = (baseConfig, env, defaultConfig) => {
  // Transpile Gatsby module because Gatsby includes un-transpiled ES6 code.
  defaultConfig.module.rules[0].exclude = [/node_modules\/(?!(gatsby)\/)/]

  // use installed babel-loader which is v8.0-beta (which is meant to work with @babel/core@7)
  defaultConfig.module.rules[0].use[0].loader = require.resolve("babel-loader")

  // use @babel/preset-react for JSX and env (instead of staged presets)
  defaultConfig.module.rules[0].use[0].options.presets = [
    require.resolve("@babel/preset-react"),
    require.resolve("@babel/preset-env"),
  ]

  defaultConfig.module.rules[0].use[0].options.plugins = [
    // use @babel/plugin-proposal-class-properties for class arrow functions
    require.resolve("@babel/plugin-proposal-class-properties"),
    // use babel-plugin-remove-graphql-queries to remove static queries from components when rendering in storybook
    require.resolve("babel-plugin-remove-graphql-queries"),
  ]

  // Prefer Gatsby ES6 entrypoint (module) over commonjs (main) entrypoint
  defaultConfig.resolve.mainFields = ["browser", "module", "main"]

  return defaultConfig
}
```
Una vez que ya tienes todo esto configurado, ejecuta Storybook para asegurarte que puede arrancar correctamente y puedes ver las historias predeterminadas instaladas por el CLI. Para correr storybook:

```shell
npm run storybook
```

El CLI de Storybook agrega este comando a tu `package.json` para que no tengas que hacer otra cosa que correr el comando. Si Storybook hace un build exitoso deberías poder navegar a `http://localhost:6006` y ver las historias por defecto provistas por el CLI de Storybook

De otro modo, si utilizas `StaticQuery` o `useStaticQuery` en tu proyecto Storybook necesita ser ejecutado con el `NODE_ENV` configurado a `production` (ya que Storybook lo configura por defecto a `development`). De otro modo `babel-plugin-remove-graphql-queries` no se ejecutará. Es más, Storybook necesita saber sobre los [archivos estáticos](https://storybook.js.org/docs/configurations/serving-static-files/#2-via-a-directory) generados por el `StaticQuery` de Gatsby. Tus scripts deberían verse como:

```json:title=package.json
{
  "scripts": {
    "storybook": "NODE_ENV=production start-storybook -s public",
    "build-storybook": "NODE_ENV=production build-storybook -s public"
  }
}
```

## Escribiendo historias

Una guía completa de escritura de historias está más allá del alcance de esta guía, pero te daremos una mirada a cómo crear una historia.

Primero, crea el archivo de historia. Storybook busca todos los archivos con extensión `.stories.js` y los carga adentro de Storybook para ti. Generalemnte querrás tus historias cerca del componente donde se definen, pero como esto es Gatsby, si quieres escribir historias para tus páginas, tendrás que crear esos mismos archivos fuera del directorio `pages`.

> Una buena solución es crear un directorio `__stories__` próximo a tu directorio `pages` y poner todas tus historias de página allí.

```jsx:title=src/components/example.stories.js
import React from "react"
import { storiesOf } from "@storybook/react"

storiesOf(`Dashboard/Header`, module).add(`default`, () => (
  <div style={{ padding: `16px`, backgroundColor: `#eeeeee` }}>
    <h1 style={{ color: "rebeccapurple" }}>Hello from Storybook and Gatsby!</h1>
  </div>
))
```

Ésta es una muy simple historia con no mucho ocurriendo, pero honestamente, nada realmente cambia con lo relacionado a Gatsby. Si quieres aprender como Storybook funciona y qué puedes hacer con él, chequea algunos de los recursos listados debajo.

## Otros recursos

- Para más información sobre Storybook, visita
  [el sitio de Storybook](https://storybook.js.org/).
- Comienza con un starter de [Jest y Storybook](https://github.com/Mathspy/gatsby-storybook-jest-starter)
