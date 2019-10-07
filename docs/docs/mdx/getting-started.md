---
title: Empezando con MDX
---

La manera más rápida de empezar con Gatsby + MDX es usar el [starter MDX](https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic). Esto te permite escribir archivos .mdx en `src/pages` para crear nuevas páginas en tu sitio.

## 🚀 Inicio Rápido

1. **Inicializar el starter MDX** con el Gatsby CLI

   ```shell
   gatsby new my-mdx-starter https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic
   ```

1. **Ejecutar el servidor de desarrollo** cambiando de directorio al sitio creado e instalar las dependencias

   ```shell
   cd my-mdx-starter/
   gatsby develop
   ```

1. **Abrir el sitio** ubicado en http://localhost:8000

1. **Actualizar el contenido MDX** abriendo la carpeta `my-mdx-starter`
   en tu editor de código fuente preferido y editar `src/pages/index.mdx`.
   Guarda tus cambios y el se actualizará automáticamente en tiempo real!

## Agregar MDX a un sitio existente de Gatsby

Si ya tienes un sitio de Gatsby al que quieras agregar MDX, podrás seguir estos paso para configurar el plugin [gatsby-plugin-mdx](/packages/gatsby-plugin-mdx/):

1. **Agregar `gatsby-plugin-mdx`** y MDX como dependencias

   ```shell
   npm install gatsby-plugin-mdx @mdx-js/mdx @mdx-js/react
   ```

   > **Nota:** Si estás actualizando desde la v0, también [revisa la guía de migración de MDX](https://mdxjs.com/migrating/v1).

1. **Actualizar tu `gatsby-config.js`** para usar`gatsby-plugin-mdx`

   ```javascript:title=gatsby-config.js
   module.exports = {
     plugins: [
       // ....
       `gatsby-plugin-mdx`,
     ],
   }
   ```

1. **Reiniciar `gatsby develop`** y agregar una página `.mdx` en `src/pages

> **Nota:** Si quieres hacer un query para frontmatter, exports, u otros campos como
> `tableOfContents` y no has agregadado un `gatsby-source-filesystem`
> dirigido a `src/pages` en tu proyecto, tendrías que agregarlo ahora.

## Próximos pasos?

Revisa [la guía de escribir MDX](/docs/mdx/writing-pages) para saber qué más puedes hacer con Gatsby y MDX.
