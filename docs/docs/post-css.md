---
title: PostCSS
---

PostCSS transforma sintaxis y características extendidas en CSS moderno y amigable para el navegador. Esta guía te mostrará cómo comenzar a usar Gatsby y PostCSS.

## Instalación y configuración de PostCSS

Esta guía asume que tienes un proyecto Gatsby configurado. Si necesitas configurar un proyecto, dirígete a la [**Guía de inicio rápido**](/docs/quick-start/) y luego, regresa.

1.  Instala el plugin Gatsby [**gatsby-plugin-postcss**](/packages/gatsby-plugin-postcss/).

`npm install --save gatsby-plugin-postcss`

2.  Incluye el plugin en tu archivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-postcss`],
```

> **Nota**: Si necesitas pasar opciones a PostCSS, usa las opciones del plugin; consulta [postcss-loader](https://github.com/postcss/postcss-loader) para ver todas las opciones disponibles.

3.  Escribe tus hojas de estilo utilizando PostCSS (archivos .css) y solicítalas o impórtalas como de costumbre.

```css:title=styles.css
@custom-media --med (width <= 50rem);

@media (--med) {
  a {
    &:hover {
      color: color-mod(black alpha(54%));
    }
  }
}
```

```javascript
import "./styles.css"
```

### Con Módulos CSS

Usar módulos CSS no requiere configuración adicional. Simplemente, antepón `.module` a la extensión. Por ejemplo: `App.css -> App.module.css`. Cualquier archivo con la extensión del módulo utilizará módulos CSS.

### Complementos PostCSS

Si prefieres agregar postprocesamiento adicional a tu PostCSS de salida, puedes especificar plugins en las opciones del complemento:

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-plugin-postcss`,
    options: {
      postCssPlugins: [require(`postcss-preset-env`)({ stage: 0 })],
    },
  },
],
```

De forma alternativa, puedes usar `postcss.config.js` para especificar tu configuración particular de PostCSS:

```javascript:title=postcss.config.js
const postcssPresetEnv = require(`postcss-preset-env`)

module.exports = () => ({
  plugins: [
    postcssPresetEnv({
      stage: 0,
    }),
  ],
})
```

## Otros recursos

- [Introducción a postcss](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)
