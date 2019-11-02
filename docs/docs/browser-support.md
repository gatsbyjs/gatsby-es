---
title: Compatibilidad Con Navegadores
---

Gatsby tiene compatibilidad con
[los mismos navegadores que la actual versión estable de React.js](https://facebook.github.io/react/docs/react-dom.html#browser-support),
la cual es actualmente IE9+, así como las versiones más recientes de otros navegadores populares.

## Polyfills

Gatsby se beneficia de la versatilidad de Babel 7 para añadir automáticamente polyfills
a tus navegadores de destino deseados.

Los navegadores recientes son compatibles con una mayor cantidad de APIs JavaScript que los navegadores
más antiguos. En el caso de versiones anteriores, Gatsby (a través de Babel) agrega automáticamente
los mínimos "polyfills" requeridos para que tu código funcione en esos navegadores.

Si comienzas a utilizar una nueva API de JavaScript como `[].includes` que no es
soportada por algunos de tus navegadores de destino deseados, no tendrás que preocuparte de que
los navegadores antiguos se rompan, ya que Babel agregará automáticamente el polyfill
necesario `core-js/modules/es7.array.includes`.

## Especifique qué navegadores soporta tu proyecto utilizando la "Browserslist"

Puedes personalizar tu lista de versiones de navegadores soportadas mediante la declaración de
la clave [`"browserslist"`](https://github.com/ai/browserslist) dentro de tu `paquete.json`.
Cambiando estos valores se modificará tus códigos de salida de JavaScript (a través de
[`babel-preset-env`](https://github.com/babel/babel-preset-env#targetsbrowsers))
y de CSS (a través de [`autoprefixer`](https://github.com/postcss/autoprefixer)).

Este artículo es una buena introducción a la emergente comunidad de herramientas que
existen en torno a la Browserslist — https://css-tricks.com/browserlist-good-idea/

Por defecto, Gatsby tiene la siguiente configuración:

```javascript:title=package.json
{
 "browserslist": [
   ">0.25%",
   "not dead"
 ]
}
```

Si usted sólo soportará navegadores más recientes, asegúrese de especificar esto en tu
`paquete.json`. Por lo general, esto te permitirá obtener archivos JavaScript más pequeños.
