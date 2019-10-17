---
title: Contribuciones al Blog y Sitio Web
---

¡Agradecemos de todo corazón las contribuciones al blog y al sitio web de Gatsby!

Aquí hay algunas cosas a tener en cuenta al decidir donde contribuir en Gatbsy:

- [Entradas en el blog](#contributing-to-the-blog) funcionan mejor para estudios de casos y la narración de historias (mira el [formato de entradas de blog](#blog-post-format)).
- [La documentación](/contributing/docs-contributions/) es material de aprendizaje continuamente relevante y reconocible que va más allá de cualquier caso de estudio o situación.
- [Cambios al sitio web](#making-changes-to-the-website) que mejoren cualquiera de estos, ¡son siempre bienvenidos!

## Contribuyendo al Blog

Nota: Antes de añadir una entrada en el blog, asegurate de tener la aprobación de un miembro del equipo de Gatsby. Puedes hacer esto [abriendo un issue](https://github.com/gatsbyjs/gatsby/issues/new/choose) o contactando con [@gatsbyjs en Twitter](https://twitter.com/gatsbyjs).

Para añadir una entrada nueva al blog de gatsbyjs.org:

- Clona el [repositorio de Gatsby](https://github.com/gatsbyjs/gatsby/) y navega a `/www`.
- Ejecuta `yarn`para instalar todas las dependencias del sitio web. ([¿Por qué Yarn?](/contributing/setting-up-your-local-dev-environment#using-yarn))
- Ejecuta `npm run develop` para previsualizar el blog en `http://localhost:8000/blog`.
- El contenido del blog reside en la carpeta `/docs/blog`. Realiza las modificaciones o añade contenido aquí.
- Añade tu imagen de avatar a `/docs/blog/avatars`.
- Añade tu nombre a `/docs/blog/author.yaml`
- Añade una nueva carpeta que siga el patrón `/docs/blog/yyyy-mm-dd-title`. Dentro de esta nueva carpeta creada, añade un fichero `index.md`.
- Añade `title`, `date`, `author`, `excerpt`, y `tags` al "frontmatter" de tu `index.md`. Puedes [ver etiquetas existentes](/blog/tags/), o [añadir una nueva](https://github.com/gatsbyjs/gatsby/blob/master/www/src/data/tags-docs.js) si sientes que tu etiqueta merece ser su propia etiqueta, aunque recomendamos que uses etiquetas existentes.
- Si estás haciendo una publicación cruzada de tu entrada en el blog, puedes añadir `canonicalLink` para beneficios en SEO. Puedes revisar otras entradas en el blog en `/docs/blog` para ejemplos
- Si tu entrada en el blog contiene imágenes, añádelas a la carpeta de la entrada en el blog y referencía estas en tu fichero `index.md` de la entrada en el blog.
- Asegúrate de que cualquier link a gatsbyjs.org es relativo - `/contributing/how-to-contribute/` en lugar de `https://gatsbyjs.org/contributing/how-to-contribute`.
- Sigue la [Guía de Estilo](/contributing/gatsby-style-guide/#word-choice) para asegurarte de que estás usando la redacción adecuada.
- Verifica tu gramática y capitaliza correctamente.
- Haz commit y push a tu fork.
- Crea una pull request desde tu rama.
  - Recomendamos usar el prefijo `docs`, p. ej. `docs/tu-cambio` or `docs-tu-cambio`. ([Ejemplo de pull request](https://github.com/gatsbyjs/gatsby/commit/9c21394add7906974dcfd22ad5dc1351a99d7ceb#diff-bf544fce773d8a5381f64c37d48d9f12))

### Formato de publicación de blog

El siguiente formato puede ayudarte a crear tu nuevo contenido en el Blog. Al inicio se encuentra el "frontmatter": un nombre elegante para metadatos en Markdown. El frontmatter de tu entrada en el Blog debe contener un título, fecha, un único nombre de autor (por ahora, agradeceríamos issues o pull requests para esto), y una o más etiquetas. Tu contenido seguirá después del segundo conjunto de guiones (`---`).

```md
---
title: "Tu increíble entrada en el Blog"
date: AAAA-MM-DD
author: Jamie Doe
excerpt: "Aquí hay un extracto útil o una breve descripción de esta publicación de blog."
tags:
  - impresionante
  - publicación
---

¡Tu próxima gran publicación de blog te espera!

Incluye imágenes creando una carpeta para tu entrada en el blog e incluyendo
Markdown y archivos de imagen para una fácil vinculación.

![increíble ejemplo](./image.jpg)
```

## Realizar cambios en el sitio web

Si quieres realizar cambios, mejoras, o añadir nueva funcionalidad al sitio web, no necesitas configurar por completo el repositorio de Gatsby para contribuir. Puedes activar tu propia instancia del sitio web de Gatsby con estos pasos:

- Clona [el repositorio de Gatsby](https://github.com/gatsbyjs/gatsby/) y navega a `/www`
- Ejecuta `yarn` para instalar todas las dependencias del sitio web.
- Ejecuta `npm run develop` para previsualizar el sitio en `http://localhost:8000/`.

> Nota: Si estas experimentando problemas en una equipo con Linux, ejecuta `sudo apt install libvips-dev`, para instalar una dependencia nativa. También puedes tomar como referencia la [guía de Gatsby en Linux](/docs/gatsby-on-linux/) para otros requerimientos específicos de Linux.

¡Ahora puedes hacer y previsualizar tus cambios antes de lanzar una pull request!

Para instrucciones para configurar el repositorio por completo, visita la página de [contribuciones de código](/contributing/code-contributions/).
