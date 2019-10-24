---
title: Envíos a la Librería de Plugins
---

## Publicando un plugin a la librería

Para agregar tu plugin a la [Librería de Plugins](/plugins/) necesitas:

1.  publicar un paquete en npm (aprende cómo [aquí](https://docs.npmjs.com/getting-started/publishing-npm-packages)),
2.  incluir los [archivos necesarios](/docs/files-gatsby-looks-for-in-a-plugin/) en el código de tu plugin,
3.  **incluir un campo de `keywords` (palabras clave)** en el `package.json` de tu plugin, conteniendo `gatsby` y `gatsby-plugin`,
4.  y documentar tu plugin con un README. Hay algunas [plantillas de plugin](/contributing/docs-templates/#plugin-readme-template) disponibles para ser usadas de referencia.

Tras seguir tales pasos, Algolia tardará 12 horas en añadir tu plugin al índice de búsquedas de la librería (el tiempo exacto aún es desconocido), y deberás esperar a que la build diaria de https://gatsbyjs.org incluya de forma automática tu página de plugin al sitio web. ¡Entonces lo único que faltará por hacer será compartir tu fabuloso plugin con la comunidad!

## Notas

### Palabras clave 

Puedes incluir otras keywords _relevantes_ a tu archivo `package.json` para ayudar a usuarios interesados a encontrar tu plugin. Por ejemplo, el transformador Markdown MathJax incluye:

```json:title=package.json
"keywords": [
  "gatsby",
  "gatsby-plugin",
  "gatsby-transformer-plugin",
  "mathjax",
  "markdown",
]
```

### Imágenes

Si incluyes imágenes en tu archivo README del repositorio de tu plugin, por favor asegúrate de referenciar la imagen con una url absoluta de modo que así salga correctamente en la página.
