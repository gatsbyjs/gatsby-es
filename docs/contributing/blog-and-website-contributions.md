---
title: Contribuciones al Blog y Sitio Web
---

¡Agradecemos de todo corazón las contribuciones al blog y al sitio web de Gatsby!

Aquí hay algunas cosas a tener en cuenta al decidir donde contribuir en Gatbsy:

- [Entradas en el blog](#contributing-to-the-blog) funcionan mejor para estudios de casos y la narración de historias (mira el [formato de entradas de blog](#blog-post-format)).
- [La documentación](/contributing/docs-contributions/) es material de aprendizaje continuamente relevante y reconocible que va más allá de cualquier caso de estudio o situación.
- [Cambios al sitio web](#making-changes-to-the-website) que mejoren cualquiera de estos, ¡son siempre bienvenidos!

## Contribuyendo al Blog

<<<<<<< HEAD
Nota: Antes de añadir una entrada en el blog, asegurate de tener la aprobación de un miembro del equipo de Gatsby. Puedes hacer esto [abriendo un issue](https://github.com/gatsbyjs/gatsby/issues/new/choose) o contactando con [@gatsbyjs en Twitter](https://twitter.com/gatsbyjs).

Para añadir una entrada nueva al blog de gatsbyjs.org:

- Clona el [repositorio de Gatsby](https://github.com/gatsbyjs/gatsby/) y navega a `/www`.
- Ejecuta `yarn` para instalar todas las dependencias del sitio web. ([¿Por qué Yarn?](/contributing/setting-up-your-local-dev-environment#using-yarn))
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
- Crea un pull request desde tu rama.
  - Recomendamos usar el prefijo `docs`, p. ej. `docs/tu-cambio` o `docs-tu-cambio`. ([Ejemplo de pull request](https://github.com/gatsbyjs/gatsby/commit/9c21394add7906974dcfd22ad5dc1351a99d7ceb#diff-bf544fce773d8a5381f64c37d48d9f12))

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
=======
If you'd like to contribute a post to the Gatsby blog, please review the process and guidelines outlined below and submit your
idea for the post to our [Gatsby blog proposal form](https://airtable.com/shr3449954866i3iF)

### Blog proposal submission process

1. Complete and submit the [Gatsby blog proposal form](https://airtable.com/shr3449954866i3iF).
2. A Gatsby team member will review your proposal and let you know if the proposal has been accepted within the next week or so.
   - **If the post is accepted:** A Gatsby team member will work with you on a timeline for submitting and reviewing a draft of your blog post and set a tentative publishing date.
   - **If the post is not accepted:** We’ll let you know if there are any alternative offers we can make (e.g. offer to retweet if you publish the piece elsewhere, suggest submitting it as an addition to a Gatsby doc, etc.). We’ll also do our best to explain why your proposal was not accepted and encourage you to revise your proposal based on that feedback and resubmit. Please don’t be discouraged from submitting another post in the future!

If you have any questions about the process or your submission, please email [marketing@gatsbyjs.com](mailto:marketing@gatsbyjs.com).

### Content guidelines for submitting a blog post proposal

As a Gatsby community member, you have unique insight into the ins and outs of learning Gatsby, building with Gatsby, and contributing to Gatsby’s open source community. Contributing to the Gatsby blog is a great way to share your experiences and insights. Here are some guidelines for what kind of content is and isn’t a good fit for the Gatsby blog.

Things we’re looking for in Gatsby blog content:

- Information to help others overcome challenges you’ve faced while working with Gatsby
- Stories about how Gatsby helped you overcome different challenges on work and personal projects
- Gatsby case studies
- Showcasing a tool, fix, or other content you or someone else have contributed to Gatsby’s open source community
- Showcasing a tool, fix, or other content someone else has contributed to Gatsby’s open source community
- Clear and thoughtful explanations of technical details or complex concepts related to React, GraphQL, web and application development, open-source contribution, Gatsby core, and other Gatsby-adjacent subject matter
- Guidance and resources for learning React, GraphQL, HTML/CSS, web development, best practices, accessibility, SEO, Gatsby, different tool and CMS integrations, and other Gatsby-adjacent subject matter.
- Other topics that you think would be valuable to people learning about or working with Gatsby

Things we’d like to avoid on the Gatsby blog:

- **Docs content.** Some content is better found in the Gatsby docs guides and tutorials, as it can be found in a section for related content and not buried under pages of other paginated blog posts.
- **Promotional content.** Please don’t submit content to the Gatsby blog solely for the purpose of promoting a product, yourself, or link-building.
  - **Here’s what you can do instead:** If you have a product or project you want to share on the Gatsby blog, focus on practical information, and make sure there’s a clear relationship with Gatsby or Gatsby-adjacent topics. You could write a step by step guide to using your product with Gatsby. You could write a case study highlighting the direct impact Gatsby had on your awesome project and offer helpful tips for others to recreate your success.
- **Content that doesn’t seem to have a clear benefit for Gatsby users and/or the Gatsby community.** For example, if you’re writing about a use-case or integration that’s extremely niche or unique to specific conditions that are really uncommon outside of your organization, the Gatsby blog might not be the best place for your content. Likewise, if your blog post doesn’t seem to have any direct relationship with Gatsby (or an interesting indirect relationship with Gatsby), then it may be more appropriate for a personal blog or another community blog.

**Please note** that these are guidelines, not rules. If you think your blog post belongs on the Gatsby blog, we absolutely encourage you to submit it. While we reserve the right to decide what is and isn’t appropriate for the Gatsby blog, we also value and encourage your creativity and your contributions.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Realizar cambios en el sitio web

Si quieres realizar cambios, mejoras, o añadir nueva funcionalidad al sitio web, no necesitas configurar por completo el repositorio de Gatsby para contribuir. Puedes activar tu propia instancia del sitio web de Gatsby con estos pasos:

- Clona [el repositorio de Gatsby](https://github.com/gatsbyjs/gatsby/) y navega a `/www`.
- Ejecuta `yarn` para instalar todas las dependencias del sitio web.
- Ejecuta `npm run develop` para previsualizar el sitio en `http://localhost:8000/`.

> Nota: Si estas experimentando problemas en una equipo con Linux, ejecuta `sudo apt install libvips-dev`, para instalar una dependencia nativa. También puedes tomar como referencia la [guía de Gatsby en Linux](/docs/gatsby-on-linux/) para otros requerimientos específicos de Linux.

¡Ahora puedes hacer y previsualizar tus cambios antes de lanzar una pull request!

Para instrucciones para configurar el repositorio por completo, visita la página de [contribuciones de código](/contributing/code-contributions/).
