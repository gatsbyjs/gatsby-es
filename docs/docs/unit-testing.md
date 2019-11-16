---
título: Prueba Unitaria
---

Las pruebas unitarias son una excelente manera de protegerse contra errores en su código antes de 
que lo desplejes. Aunque Gatsby no incluye soporte para pruebas unitarias 
inusuales, solo toma unos pocos pasos para comenzar a funcionar. Sin embargo, hay algunas 
características del proceso de compilación de Gatsby que hacen que la configuración estándar de Jest no
funciona del todo. Esta guía le muestra cómo configurarlo.

## Configurando su entorno

El _framework_ de prueba más popular para React es [Jest](https://jestjs.io/),
que fue creado por Facebook. Aunque Jest es un _framework_ de pruebas unitarias de JavaScript de 
propósito general, tiene muchas características que lo hacen funcionar particularmente bien
con React.

_Nota: Para esta guía, comenzarás con `gatsby-starter-default`, pero los conceptos deben ser los mismos o muy similares para su sitio._

### 1. Instalar dependencias

Primero, necesitas instalar Jest y algunos paquetes más necesarios. Instale babel-jest y babel-preset-gatsby para asegurarse de que los preajustes de babel que se utilizan coinciden con los que se utilizan internamente para su sitio Gatsby.

```shell
npm install --save-dev jest babel-jest react-test-renderer babel-preset-gatsby identity-obj-proxy
```

### 2. Crear un archivo de configuración para Jest

Debido a que Gatsby maneja su propia configuración de Babel, tú deberás decirle
manualmente a Jest que use `babel-jest`. La forma más fácil de hacer esto es añadiendo `jest.config.js`. Tú puedes configurar algunos valores predeterminados útiles al mismo tiempo:

```js:title=jest.config.js
module.exports = {
  transform: {
    "^.+\\.jsx?$": `<rootDir>/jest-preprocess.js`,
  },
  moduleNameMapper: {
    ".+\\.(css|styl|less|sass|scss)$": `identity-obj-proxy`,
    ".+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": `<rootDir>/__mocks__/file-mock.js`,
  },
  testPathIgnorePatterns: [`node_modules`, `.cache`, `public`],
  transformIgnorePatterns: [`node_modules/(?!(gatsby)/)`],
  globals: {
    __PATH_PREFIX__: ``,
  },
  testURL: `http://localhost`,
  setupFiles: [`<rootDir>/loadershim.js`],
}
```

Repasemos el contenido de este archivo de configuración:

- La sección `transform` le indica a Jest que todos los archivos `js` o `jsx` deben ser
  transformados usando un archivo `jest-preprocess.js` en la raíz del proyecto. Sigue adelante y
 crea este archivo ahora. Aquí es donde configuras tú configuración de Babel. Tú puedes empezar
 con la siguiente configuración mínima:

```js:title=jest-preprocess.js
const babelOptions = {
  presets: ["babel-preset-gatsby"],
}

module.exports = require("babel-jest").createTransformer(babelOptions)
```

- La siguiente opción es `moduleNameMapper`. Esta
  sección funciona un poco como las reglas de webpack,  y le dice a Jest cómo manejar las importaciones.
  Aquí te preocupa principalmente simular las importaciones de archivos estáticos, porque Jest no las puede
  manejar. Un simulacro es un módulo ficticio que se utiliza en lugar del módulo real dentro 
  las pruebas. Es bueno cuando tienes algo que no puedes o no quieres probar.
  Puedes simular cualquier cosa, y aquí estás simulando los activos en lugar del del código. Para
  hojas de estilo necesita usar el paquete `identity-obj-proxy`. Para todos los otros activos
  necesitas usar un simulacro manual llamado `file-mock.js`. Necesitas crear esto tú mismo.
  La convención es crear un directorio llamado `__mocks__` en el directorio raíz
  para esto. Ten en cuenta el par de guiones bajos dobles en el nombre.

```js:title=__mocks__/file-mock.js
module.exports = "test-file-stub"
```

- La siguiente configuración es `testPathIgnorePatterns`. Le estás diciendo a Jest que ignore
  cualquier prueba en los directorios `node_modules` o `.cache`.

- La siguiente opción es muy importante y es diferente de lo que encontrarás en otras
  guías de Jest. La razón por la que necesitas `transformIgnorePatterns` es porque Gatsby
  incluye código ES6 no transpilado. Con la configuracion _default_ de Jest, no transforma el código
  dentro de `node_modules`, entonces vas a obtener un error come este:

```
/my-app/node_modules/gatsby/cache-dir/gatsby-browser-entry.js:1
({"Object.<anonymous>":function(module,exports,require,__dirname,__filename,global,jest){import React from "react"
                                                                                            ^^^^^^
SyntaxError: Unexpected token import
```

Esto se debe a que `gatsby-browser-entry.js` no se transpila antes de ejecutarse
en Jest. Puedes arreglar esto cambiando el valor predeterminado `transformIgnorePatterns` a
excluir el módulo `gatsby`.

- La sección `globals` establece `__PATH_PREFIX__`, que generalmente lo establece Gatsby,
  y que algunos componentes necesitan.

- Debe establecer `testURL` con una URL válida,  porque algunos APIs de DOM como
  `localStorage` no le son suficiente los valores prederminados (`about:blank`).

> Nota: si está utilizando Jest 23.5.0 o posterior, `testURL` usará `http://localhost` entonces puedes omitir esta configuración.

- Hay un global más que debes configurar, pero como es una función no puedes
  configúrelo aquí en el JSON. El `setupFiles` _array_ te permite enumerar los archivos que serán
  incluido antes de ejecutar todas las pruebas, por lo que es perfecto para esto.

```js:title=loadershim.js
global.___loader = {
  enqueue: jest.fn(),
}
```

### 3. Simulacros útiles para completar su entorno de prueba

#### Simulando `gatsby`

Finalmente, es una buena idea simular el module `gatsby`. Esto puede no ser
necesario al principio, pero hará las cosas mucho más fáciles si quieres probar
componentes que usan `Link` o GraphQL.

```js:title=__mocks__/gatsby.js
const React = require("react")
const gatsby = jest.requireActual("gatsby")

module.exports = {
  ...gatsby,
  graphql: jest.fn(),
  Link: jest.fn().mockImplementation(
    // these props are invalid for an `a` tag
    ({
      activeClassName,
      activeStyle,
      getProps,
      innerRef,
      partiallyActive,
      ref,
      replace,
      to,
      ...rest
    }) =>
      React.createElement("a", {
        ...rest,
        href: to,
      })
  ),
  StaticQuery: jest.fn(),
  useStaticQuery: jest.fn(),
}
```

Esto simula la función `graphql()`, el componente `Link`, y el componente `StaticQuery`.

## Pruebas de escritura

Una guía completa de pruebas unitarias está más allá del ámbito de esta guía, pero tú puedes 
empezar con una simple prueba instantánea para verificar que todo esté funcionando.

Primero, crea un archivo de prueba. Los puedes poner en el directorio 
`__tests__`, en otro lugar (generalmente al lado del componente en sí), con
la extensión `.spec.js` o `.test.js`. La decisión está basada en tú
preferencia. En esta guía, utilizaremos la convención de carpetas `__tests__`. Creemos una prueba para nuestro componente de encabezado, así que cree un archivo `header.js` en `src/components/__tests__/`:

```js:title=src/components/__tests__/header.js
import React from "react"
import renderer from "react-test-renderer"

import Header from "../header"

describe("Header", () => {
  it("renders correctly", () => {
    const tree = renderer
      .create(<Header siteTitle="Default Starter" />)
      .toJSON()
    expect(tree).toMatchSnapshot()
  })
})
```

Esta es una prueba instantánea muy simple, que usa `react-test-renderer` para rederizar
el componente y luego genera un _snapshot_ de él mismo en la primera ejecución. Luego
compara los futuros _snapshots_ contra este, lo que significa que puede verificar rápidamente por
regresiones. Visite [los documentos de Jest](https://jestjs.io/docs/en/getting-started) para
aprender más sobre otras pruebas que tú puedes escribir.

## Ejecutando pruebas

Si miras dentro de `package.json`, probablemente encontrarás que ya hay un
_script_ para `test`, que solo muestra un mensaje de error. Cambie esto para usar el
ejecutable `jest` que ahora tenemos disponible, así:

```json:title=package.json
  "scripts": {
    "test": "jest"
  }
```

Esto significa que ahora puede ejecutar pruebas escribiendo `npm test`. Si quieres, puedes
también ejecutar con un indicador que activa el modo de observación para ver archivos y ejecutar pruebas cuando se cambian: `npm test -- --watch`.

¡Ejecute las pruebas nuevamente y todo debería funcionar! Tú puedes recibir un mensaje sobre
el _snapshot_ que se está escribiendo. Esto se crea en un directorio `__snapshots__` seguido
a tus pruebas. Si lo miras, verás que es una representación JSON
del componente `<Header />`. Debe verificar sus archivos de _snapshots_
en un sistema de control de fuente (por ejemplo, un repositorio de GitHub) para que cualquier cambio se rastree en el historial.
Esto es particularmente importante para recordar si está utilizando un continuo
sistema de integración como Travis o CircleCI para ejecutar pruebas, ya que fallarán si el _snapshot_ no se registra en el control de origen.

Si realiza cambios que necesiten actualizar el _snapshot_, puede hacerlo
ejecutando `npm test - -u`.

## Usando TypeScript

Si está utilizando TypeScript, necesita hacer un par de pequeños cambios en su
configuración.  Primero instale `ts-jest`:

```shell
npm install --save-dev ts-jest
```

Luego actualice la configuración en `jest.config.js`, así:

```js:title=jest.config.js
module.exports = {
  transform: {
    "^.+\\.tsx?$": "ts-jest",
    "^.+\\.jsx?$": "<rootDir>/jest-preprocess.js",
  },
  testRegex: "(/__tests__/.*|(\\.|/)(test|spec))\\.([tj]sx?)$",
  moduleNameMapper: {
    ".+\\.(css|styl|less|sass|scss)$": "identity-obj-proxy",
    ".+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$":
      "<rootDir>/__mocks__/file-mock.js",
  },
  moduleFileExtensions: ["ts", "tsx", "js", "jsx", "json", "node"],
  testPathIgnorePatterns: ["node_modules", ".cache", "public"],
  transformIgnorePatterns: ["node_modules/(?!(gatsby)/)"],
  globals: {
    __PATH_PREFIX__: "",
  },
  testURL: "http://localhost",
  setupFiles: ["<rootDir>/loadershim.js"],
}
```

Tu puedes notar que hay otras dos opciones, , `testRegex` y `moduleFileExtensions`,
han sido agregados. La opción `testRegex` es el patrón que le dice a Jest qué archivos
contienen pruebas. El patrón anterior coincide con cualquier archivo`.js`, `.jsx`, `.ts` o `.tsx`
dentro de un directorio`__tests__`, o cualquier archivo en otro lugar con la extensión
`.test.js`, `.test.jsx`, `.test.ts`, `.test.tsx`, o `.spec.js`, `.spec.jsx`,
`.spec.ts`, `.spec.tsx`.
s ne
La opción `moduleFileExtensions` es necesaria cuando se trabaja con TypeScript.
Lo único que hace es decirle a Jest qué extensiones de archivo puede
importar en sus archivos sin precisar la extensión del archivo. Con la configuración inicial,
funciona con las extensiones de archivo `js`,` json`, `jsx`,` node`, por lo que solo necesitamos
agregar `ts` y` tsx`. Puede leer más al respecto en [la documentación de Jest](https://jestjs.io/docs/en/configuration.html#modulefileextensions-array-string).

## Otros recursos

Si necesita hacer cambios en su configuración de Babel, tú puedes editar la configuración en
`jest-preprocess.js`. Es posible que debes habilitar algunos de los complementos utilizados por Gatsby,
aunque recuerde que puede que necesite instalar las versiones de Babel 7. Vea
[la guía de configuración de Gatsby Babel](/docs/babel) para algunos ejemplos.

Para obtener más información sobre las pruebas de Jest, visita
[el sitio de Jest](https://jestjs.io/docs/en/getting-started).

Para ver un ejemplo que encapsula todas estas técnicas--y un conjunto de pruebas de unidad completa con [@testing-library/react][react-testing-library], consulte el ejemplo [using-jest][using-jest].

[using-jest]: https://github.com/gatsbyjs/gatsby/tree/master/examples/using-jest
[react-testing-library]: https://github.com/testing-library/react-testing-library
