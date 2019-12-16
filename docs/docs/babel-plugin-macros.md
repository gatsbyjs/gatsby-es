---
title: Usando el plugin macros babel
---

Gatsby incluye una poderosa y nueva manera de aplicar transformaciones de código en
tiempo-de-compilación,
[Macros babel](https://github.com/kentcdodds/babel-plugin-macros)! Las macros son
como plugins Babel, pero en vez de agregarlas a tu `.babelrc`, las importas en
el archivo que quieres que las use. Esto tiene dos grandes ventajas:

- No confusiones por no saber de donde viene una sintaxis no-estándar. Las macros son
  importadas explícitamente donde son usadas.
- No archivos de configuración. Las macros son incluidas directamente en tú código según se necesiten.

Como los plugins Babel, las macros se ejecutan solo en tiempo de compilación. No son incluidas en
el bundle Javascript público. Por lo cual, las macros no tienen ningún efecto en tú código
más allá de la transformación que aplican.

## Instalando macros

Justo como plugins, muchas macros son publicadas como paquetes npm. Por convención,
son nombradas por su función, seguidas de `.macro`.

Por ejemplo, [`preval.macro`](https://www.npmjs.com/package/preval.macro) es una
macro que pre-evaluá el código Javascript. Puedes instalarla ejecutando:

```shell
npm install --save-dev preval.macro
```

Algunas macros son incluidas en paquetes más grandes. Para instalarlas y usarlas,
refierete a su documentación.

## Usando macros

Para usar una macro instalada, impórtala en tu código:

```javascript
import preval from "preval.macro"
```

Entonces puedes usar la variable importada aunque la documentación de la macro dice.
`preval.macro` es usada como una etiqueta de plantilla literal:

```javascript
import preval from "preval.macro"
const x = preval`module.exports = 1` // highlight-line
```

Cuando compiles tu proyecto este código sera transformado a:

```javascript
const x = 1
```

## Descubriendo macros disponibles

Echa un vistazo a la lista
[Macros babel asombrosas](https://github.com/jgierer12/awesome-babel-macros)
para encontrar las macros disponibles que puedes usar. Adicionalmente, la lista contiene
recursos de mucha ayuda para usar macros y desarrollarlas tú mismo.
