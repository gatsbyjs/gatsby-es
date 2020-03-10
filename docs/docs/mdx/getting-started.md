---
title: Empezando con MDX
---

La manera más rápida de empezar con Gatsby + MDX es usar el [starter MDX](https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic). Esto te permite escribir archivos .mdx en `src/pages` para crear nuevas páginas en tu sitio.

## 🚀 Inicio Rápido

1. **Inicializar el starter MDX** con la CLI de Gatsby

   ```shell
   gatsby new mi-mdx-starter https://github.com/ChristopherBiscardi/gatsby-starter-mdx-basic
   ```

1. **Ejecutar el servidor de desarrollo** cambiando de directorio al sitio creado e instalar las dependencias

   ```shell
   cd mi-mdx-starter/
   gatsby develop
   ```

2. **Abrir el sitio** ubicado en `http://localhost:8000`

3. **Actualizar el contenido MDX** abriendo la carpeta `mi-mdx-starter`
   en tu editor de código preferido y editando `src/pages/index.mdx`.
   Guarda los cambios y el navegador se actualizará automáticamente en tiempo real!

## Agregar MDX a un sitio existente creado con Gatsby

Si ya tienes un sitio creado con Gatsby al que le quieras agregar MDX, puedes 
seguir estos pasos para configurar el plugin [gatsby-plugin-mdx](/packages/gatsby-plugin-mdx/):

Alternativamente, puedes que quieras configurar un sitio de blog existente para usar MDX. [Este blog post](/blog/2019-11-21-how-to-convert-an-existing-gatsby-blog-to-use-mdx/) te guia por esos pasos en detalle.

1. **Agregar `gatsby-plugin-mdx`** y MDX como dependencias

   ```shell
   npm install gatsby-plugin-mdx @mdx-js/mdx @mdx-js/react
   ```

   > **Nota:** Si estás actualizando desde la v0, también [revisa la guía de migración de MDX](https://mdxjs.com/migrating/v1).

2. **Actualiza tu `gatsby-config.js`** para usar`gatsby-plugin-mdx`

   ```javascript:title=gatsby-config.js
   module.exports = {
     plugins: [
       // ....
       `gatsby-plugin-mdx`,
     ],
   }
   ```

3. **Reinicia `gatsby develop`** y agregar una página `.mdx` en `src/pages

> **Nota:** Si quieres hacer una query para frontmatter, exports, u otros campos como
> `tableOfContents` y no has agregadado un `gatsby-source-filesystem`
> que apunte a `src/pages` en tu proyecto, tendrías que agregarlo ahora.

## Próximos pasos?

Revisa [la guía para escribir MDX](/docs/mdx/writing-pages) para saber qué más puedes hacer con Gatsby y MDX.
