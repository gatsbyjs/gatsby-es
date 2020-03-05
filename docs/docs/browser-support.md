---
title: Compatibilidad Con Navegadores
---

Gatsby tiene compatibilidad con [los mismos navegadores que la actual versión estable de React.js](https://facebook.github.io/react/docs/react-dom.html#browser-support), la cual es actualmente IE9+, así como las versiones más recientes de otros navegadores populares.

## Polyfills

Gatsby se beneficia de la versatilidad de Babel 7 para añadir automáticamente polyfills a tus navegadores de destino deseados.

Los navegadores recientes son compatibles con una mayor cantidad de APIs JavaScript que los navegadores más antiguos. En el caso de versiones anteriores, Gatsby (a través de Babel) agrega automáticamente los mínimos "polyfills" requeridos para que tu código funcione en esos navegadores.

Si comienzas a utilizar una nueva API de JavaScript como `[].includes` que no es compatible con algunos de tus navegadores de destino deseados, no tendrás que preocuparte de que los navegadores antiguos se rompan, ya que Babel agregará automáticamente el polyfill necesario `core-js/modules/es7.array.includes`.

## Especifica qué navegadores son compatibles con tu proyecto utilizando la "Browserslist"

Puedes personalizar tu lista de versiones de navegadores compatibles mediante la declaración de la clave [`"browserslist"`](https://github.com/ai/browserslist) dentro de tu `package.json`. Cambiando estos valores se modificará tu código de JavaScript (a través de [`babel-preset-env`](https://github.com/babel/babel-preset-env#targetsbrowsers)) y de CSS (a través de [`autoprefixer`](https://github.com/postcss/autoprefixer)) de salida.

Este artículo es una buena introducción a la emergente comunidad de herramientas que existen en torno a la Browserslist — https://css-tricks.com/browserlist-good-idea/

Por defecto, Gatsby tiene la siguiente configuración:

```json:title=package.json
{
  "browserslist": [">0.25%", "not dead"]
}
```

Si sólo quieres dar compatibilidad con navegadores más recientes, asegurate de especificar esto en tu `package.json`. Por lo general, esto te permitirá obtener archivos JavaScript más pequeños.
