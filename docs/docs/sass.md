---
title: Uso de Sass en Gatsby
---

[Sass](https://sass-lang.com) es una extensión de CSS, que agrega reglas anidadas, variables, mixins, herencia de selectores y más. En Gatsby, el código Sass se puede traducir a CSS estándar, en el formato correcto, mediante un complemento.

Sass compilará los archivos `.sass` y `.scss` en archivos `.css`, para que puedas escribir tus hojas de estilo con funciones más avanzadas.

> **Nota**: la diferencia entre usar un archivo `.sass` o `.scss` es la sintaxis en la que escribes tus estilos. Todo CSS válido es también SCSS válido, por lo que es el más fácil de usar y el más popular . Puedes leer más sobre las diferencias en la [documentación de Sass](https://sass-lang.com/documentation/syntax).

## Instalación y configuración de Sass

Esta guía asume que tienes un proyecto Gatsby configurado. Si necesitas configurar un proyecto, dirígete a la [**Guía de inicio rápido**](/docs/quick-start/) y luego, regresa.

1.  Instala el plugin Gatsby [**gatsby-plugin-sass**](/packages/gatsby-plugin-sass/) y `node-sass`, una dependencia obligatoria requerida a partir de v2.0.0.

`npm install --save node-sass gatsby-plugin-sass`

2.  Incluye el complemento en tu archivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

> **Nota**: Puedes configurar [opciones adicionales del complemento](/packages/gatsby-plugin-sass/#other-options) como rutas para incluir y opciones para `css-loader`.

3.  Escribe tus hojas de estilo como archivos `.sass` or `.scss` y solicítalas o impórtalas como de costumbre.

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

## Otros recursos

- [Introducción a Sass](https://designmodo.com/introduction-sass/)
- [Documentación de Sass](https://sass-lang.com/documentation)
- [Gatsby *starters* que usan Sass](/starters/?c=Styling%3ASCSS)
