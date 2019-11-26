---
title: Using Sass in Gatsby
---

[Sass](https://sass-lang.com) es una extensión de CSS, que agrega reglas anidadas, variables, mixins, herencia de selectores y más. En Gatsby, el código Sass se puede traducir a CSS estándar, en el formato correcto, mediante un plugin.

Sass will compile `.sass` and `.scss` files to `.css` files for you, so you can write your stylesheets with more advanced features.

> **Nota**: la diferencia entre usar un archivo `.sass` o `.scss` es la sintaxis en la que escribes tus estilos. Todo CSS válido es también SCSS válido, por lo que es el más fácil de usar y el más popular. Puedes leer más sobre las diferencias en la [documentación de Sass](https://sass-lang.com/documentation/syntax).

## Installing and Configuring Sass

This guide assumes that you have a Gatsby project set up. If you need to set up a project, head to the [**Quick Start guide**](/docs/quick-start/), then come back.

1.  Instala el plugin Gatsby [**gatsby-plugin-sass**](/packages/gatsby-plugin-sass/) y `node-sass`, una dependencia obligatoria requerida a partir de v2.0.0.

`npm install --save node-sass gatsby-plugin-sass`

2.  Incluye el plugin en tu archivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

> **Nota**: Puedes configurar [opciones adicionales del plugin](/packages/gatsby-plugin-sass/#other-options) como rutas para incluir y opciones para `css-loader`.

3.  Write your stylesheets as `.sass` or `.scss` files and require or import them as normal.

```css:styles.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css:styles.sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```javascript
import "./styles.scss"
import "./styles.sass"
```

## Other resources

- [Introducción a Sass](https://designmodo.com/introduction-sass/)
- [Documentación de Sass](https://sass-lang.com/documentation)
- [*Starters* de Gatsby que usan Sass](/starters/?c=Styling%3ASCSS)
