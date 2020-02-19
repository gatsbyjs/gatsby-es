---
title: Compatibilidad Con Navegadores
---

<<<<<<< HEAD
Gatsby tiene compatibilidad con
[los mismos navegadores que la actual versión estable de React.js](https://facebook.github.io/react/docs/react-dom.html#browser-support),
la cual es actualmente IE9+, así como las versiones más recientes de otros
navegadores populares.

## Polyfills

Gatsby se beneficia de la versatilidad de Babel 7 para añadir automáticamente polyfills
a tus navegadores de destino deseados.

Los navegadores recientes son compatibles con una mayor cantidad de APIs JavaScript que los navegadores
más antiguos. En el caso de versiones anteriores, Gatsby (a través de Babel) agrega automáticamente
los mínimos "polyfills" requeridos para que tu código funcione en esos navegadores.

Si comienzas a utilizar una nueva API de JavaScript como `[].includes` que no es
compatible con algunos de tus navegadores de destino deseados, no tendrás que preocuparte de que
los navegadores antiguos se rompan, ya que Babel agregará automáticamente el polyfill
necesario `core-js/modules/es7.array.includes`.
=======
Gatsby supports [the same browsers as the current stable version of React.js](https://facebook.github.io/react/docs/react-dom.html#browser-support) which is currently IE9+ as well as the most recent versions of other popular browsers.

## Polyfills

Gatsby leverages Babel 7's ability to automatically add polyfills for your target browsers.

Newer browsers support more JavaScript APIs than older browsers. For older versions, Gatsby (via Babel) automatically adds the minimum "polyfills" necessary for your code to work in those browsers.

If you start using a newer JavaScript API like `[].includes` that isn't supported by some of your targeted browsers, you won't have to worry about it breaking the older browsers as Babel will automatically add the needed polyfill `core-js/modules/es7.array.includes`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Especifica qué navegadores son compatibles con tu proyecto utilizando la "Browserslist"

<<<<<<< HEAD
Puedes personalizar tu lista de versiones de navegadores compatibles
mediante la declaración de la clave [`"browserslist"`](https://github.com/ai/browserslist)
dentro de tu `package.json`. Cambiando estos valores se modificará tu código de
JavaScript (a través de
[`babel-preset-env`](https://github.com/babel/babel-preset-env#targetsbrowsers))
y de CSS (a través de [`autoprefixer`](https://github.com/postcss/autoprefixer)).

Este artículo es una buena introducción a la emergente comunidad de herramientas que
existen en torno a la Browserslist — https://css-tricks.com/browserlist-good-idea/
=======
You may customize your list of supported browser versions by declaring a [`"browserslist"`](https://github.com/ai/browserslist) key within your `package.json`. Changing these values will modify your JavaScript (via[`babel-preset-env`](https://github.com/babel/babel-preset-env#targetsbrowsers)) and your CSS (via [`autoprefixer`](https://github.com/postcss/autoprefixer)) output.

This article is a good introduction to the growing community of tools around Browserslist — https://css-tricks.com/browserlist-good-idea/
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Por defecto, Gatsby tiene la siguiente configuración:

```json:title=package.json
{
  "browserslist": [">0.25%", "not dead"]
}
```

<<<<<<< HEAD
Si sólo quieres dar compatibilidad con navegadores más recientes, asegurate de especificar esto en tu
`package.json`. Por lo general, esto te permitirá obtener archivos JavaScript más pequeños.
=======
If you only support newer browsers, make sure to specify this in your `package.json`. This will often enable you to ship smaller JavaScript files.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc
