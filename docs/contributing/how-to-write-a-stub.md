---
title: Cómo escribir un stub
---

Tal vez tienes una idea para una página de documentación de Gatsby.js o estás de acuerdo con una sugerencia en un Issue de GitHub, pero no tienes el tiempo o los recursos para escribir esa página. En vez de dejar que la idea se te desvanezca, considera **crear un stub de documentación** como una reserva del contenido venidero. Así otros miembros de la comunidad (y/o tú en el futuro) pueden regresar y rellenar los detalles.

Un **stub** es una reserva temporal para una página de documentación de Gatsby.js enlazado con un Issue de GitHub, que utiliza esta plantilla (puedes copiarla y pegarla, cambiando el título y el número del Issue):

```markdown:title=how-to-tame-dragons.md
---
title: How to Tame Dragons
issue: https://github.com/gatsbyjs/gatsby/issues/XXXX
---

This is a stub. Help our community expand it.

Please use the [Gatsby Style Guide](/contributing/gatsby-style-guide/) to ensure your
pull request gets accepted.
```

Si tienes cualquier pregunta sobre títulos u otros detalles en relación a crear stubs, por favor pregúntanos en el Issue de Github pertinente.

## Sesiones de programación en pareja de la comunidad

Si llegas a crear un stub o ves uno en el sitio de Gatsby.js y te interesa rellenar el contenido, fíjate en el [programa de Programación en pareja](/contributing/pair-programming/) de Gatsby.js. Nos encantaría trabajar contigo en tu aventura de contribuir al código-abierto!

## Convertir un stub en un documento

Para transformar el stub en un documento viviente, quita la etiqueta `issue` del frontmatter (los metadatos de Markdown) del stub, y reemplaza el texto modelo con tu código y prosa bella. Guarda el archivo, sube un commit a GitHub, abre un pull request, y busca feedback. Aprende más en nuestra página sobre [contribuciones a los docs](/contributing/docs-contributions/).

Si te gustaría ver los stubs disponibles, visita la [Lista de stubs](/contributing/stub-list/).
