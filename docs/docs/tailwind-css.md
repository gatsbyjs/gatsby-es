---
title: Tailwind CSS
---

Tailwind es un _framework_ CSS, del tipo _utility-first_, para crear rápidamente interfaces de usuario personalizadas. Esta guía te mostrará cómo comenzar a usar Gatsby y [Tailwind CSS](https://tailwindcss.com/).

## Visión general

Hay tres formas de usar Tailwind con Gatsby:

1. Estándar: Usa PostCSS para generar clases de Tailwind, luego podrás aplicar esas clases usando `className`.
2. _CSS-in-JS_: Integra clases de Tailwind dentro de _Styled Components_.
3. SCSS: Usa [gatsby-plugin-sass](/packages/gatsby-plugin-sass) para dar compatibilidad a clases Tailwind en tus archivos SCSS.

Para estos métodos, deberás instalar y configurar Tailwind, por lo que esta guía te guiará primero por ese paso, luego podrás seguir las instrucciones para PostCSS, CSS-in-JS o SCSS.

## Instalar y configurar Tailwind

Esta guía asume que tienes un proyecto Gatsby configurado. Si necesitas configurar un proyecto, dirígete a la [**Guía de inicio rápido**](/docs/quick-start), y luego regresa.

1. Instala Tailwind

```shell
npm install tailwindcss --save-dev
```

2. Genera el archivo de configuración de Tailwind (opcional)

**Nota**: No se requiere un archivo de configuración para Tailwind 1.0.0+

Para configurar Tailwind, necesitaremos agregar un archivo de configuración de Tailwind. Afortunadamente, Tailwind tiene un script incorporado para hacer esto. Simplemente ejecuta el siguiente comando:

```shell
npx tailwind init
```

### Opción #1: PostCSS

1.  Instala el plugin Gatsby PostCSS [**gatsby-plugin-postcss**](/packages/gatsby-plugin-postcss).

```shell
npm install --save gatsby-plugin-postcss
```

1.  Incluye el plugin en tu archivo `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-postcss`],
```

3. Configura PostCSS para usar Tailwind

Crea un archivo `postcss.config.js` en la carpeta raíz de tu proyecto con los siguientes contenidos.

```javascript:title=postcss.config.js
module.exports = () => ({
  plugins: [require("tailwindcss")],
})
```

4. Usa las directivas de Tailwind en tu CSS

Ahora puedes usar las directivas `@tailwind` para agregar las utilidades de Tailwind, la verificación previa y los componentes a tu CSS. ¡También puedes usar `@apply` y todas las demás directivas y funciones de Tailwind!

Para obtener más información sobre cómo usar Tailwind en tu CSS, visita la [Documentación de Tailwind](https://tailwindcss.com/docs/installation#3-use-tailwind-in-your-css)

### Opción #2: CSS-in-JS

Estos pasos suponen que ya tienes instalada una biblioteca CSS-in-JS, y los ejemplos se basan en _Styled Components_.

1. Instala el Macro de Babel para Tailwind

**Nota**: Actualmente, `tailwind.macro` no es compatible con Tailwind 1.0.0+. Sin embargo, hay una versión beta compatible, disponible en `tailwind.macro@next`. Tómate la libertad de usar la versión beta o volver a TailwindCSS 0.7.4.

**Opción 1**: Instala `tailwind.macro@next` y usa Tailwind 1.0.0+

```shell
npm install --save tailwind.macro@next
```

**Opción 2**: Instala `tailwind.macro` estable y usa Tailwind 0.7.4

```bash
// Desinstala tailwind 1.0.0+ sí ya lo tenías instalado
npm uninstall tailwindcss

// Instala tailwind 0.7.4 y la versión estable de tailwind.macro
npm install tailwindcss@0.7.4
npm install tailwind.macro
```

1. Usa el Macro de Babel (`tailwind.macro`) en tu componente con _Styled Components_

```javascript
import styled from "styled-components"
import tw from "tailwind.macro"

// Todas las versiones
const Button = styled.button`
  ${tw`bg-blue hover:bg-blue-dark text-white p-2 rounded`};
`

// tailwind.macro@next
const Button = tw.button`
  bg-blue hover:bg-blue-dark text-white p-2 rounded
`
```

### Opción #3: SCSS

1.- Instala el plugin de SCSS de Gatsby [**gatsby-plugin-sass**](/packages/gatsby-plugin-sass) y `node-sass`.

```shell
npm install --save node-sass gatsby-plugin-sass
```

2.- Para poder usar clases de Tailwind en tus archivos SCSS, agrega el paquete `tailwindcss` dentro del parámetro `postCSSPlugins` en tu `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-plugin-sass`,
    options: {
      postCssPlugins: [
        require("tailwindcss"),
        require("./tailwind.config.js"), // Opcional: Cargar una configuración personalizada de Tailwind
      ],
    },
  },
],
```

**Nota:** Opcionalmente puedes agregar un archivo de configuración correspondiente (por defecto será `tailwind.config.js`).
Sí estás agregando una configuración personalizada, necesitarás cargarla después de `tailwindcss`.

## Otros recursos

- [Introducción a PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)
- [Documentación de Tailwind](https://tailwindcss.com/)
- [*Starters* de Gatsby que usan Tailwind](/starters/?c=Styling%3ATailwind&v=2)
