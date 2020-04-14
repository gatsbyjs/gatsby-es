---
title: Contribuciones al Blog y Sitio Web
---

¡Agradecemos de todo corazón las contribuciones al blog y al sitio web de Gatsby!

Aquí hay algunas cosas a tener en cuenta al decidir donde contribuir en Gatbsy:

- [Entradas en el blog](#contributing-to-the-blog) funcionan mejor para estudios de casos y la narración de historias (mira el [formato de entradas de blog](#blog-post-format)).
- [La documentación](/contributing/docs-contributions/) es material de aprendizaje continuamente relevante y reconocible que va más allá de cualquier caso de estudio o situación.
- [Cambios al sitio web](#making-changes-to-the-website) que mejoren cualquiera de estos, ¡son siempre bienvenidos!

## Contribuyendo al Blog

Sí te gustaría contribuir con un post en el blog de Gatsby, por favor revisa el proceso y las pautas descritas abajo para enviar
tu idea para el post a nuestro [formulario de propuestas para el blog de Gatsby](https://airtable.com/shr3449954866i3iF)

### Proceso de presentación de propuesta de Blog

1. Completa y envía el [formulario de propuesta para el blog de Gatsby](https://airtable.com/shr3449954866i3iF).
2. Un miembro del equipo de Gatsby revisará tu propuesta y te hará saber sí la propuesta fue aceptada en un lapso de una semana aproximadamente.
   - **Sí el post es aceptado:** Un miembro del equipo de Gatsby trabajará contigo en un cronograma para enviar y revisar un borrador del post del blog y acordar una fecha tentativa de publicación.
   - **Sí el post no es aceptado:** Te haremos saber sí existe alguna oferta alternativa que podamos ofrecer (p.ej hacer retweet sí publicas el post en algun otro blog, sugerir publicarlo como una adición a alguna documentación de Gatsby, etc.). También haremos lo posible para explicar por qué la propuesta no fue aceptada y animarte a revisar tu propuesta de acuerdo a la retroalimentación y volverla a enviar. ¡Por favor no te desanimes a enviar otro post en el futuro!

Sí tienes alguna pregunta sobre nuestro proceso o sobre tu propuesta, por favor envía un correo electrónico a [marketing@gatsbyjs.com](mailto:marketing@gatsbyjs.com).

### Pautas de contenido para enviar una propuesta de post al blog

Como un miembro de la comunidad de Gatsby, tienes una visión única de los pros y contras de aprender Gatsby, construir con Gatsby y contribuir a la comunidad _open source_ Gatsby. Contribuir al blog de Gatsby es una manera increíble de compartir tus experiencias y puntos de vista. Aquí hay algunas pautas del tipo de contenido que encaja y no encaja con el blog de Gatsby.

Cosas que buscamos para el contenido del blog de Gatsby:

- Información para ayudar a otros a superar desafíos que te has encontrado antes mientras trabajabas con Gatsby
- Historias sobre como Gatsby te ha ayudado a superar diferentes desafíos en proyectos personales y del trabajo
- Casos de estudio con Gatsby
- Mostrar una herramienta, un fix, u otro contenido que tu u otra persona ha contribuido a la comunidad _open source_ de Gatsby
- Mostrar una herramienta, un fix que otra persona ha contribuido a la comunidad _open source_ de Gatsby
- Explicaciones claras y concisas de detalles técnicos o conceptos complejos relacionados con React, GraphQL, la web y desarrollo de aplicaciones, contribuciones _open source_, core de Gatsby y temas relacionados con Gatsby.
- Otros temas que piensas que podrían ser valiosos para las personas aprendiendo o trabajando con Gatsby.

Cosas que queremos evitar en el blog de Gatsby:

- **Contenido de la documentación.** Algunos contenidos es mejor encontrarlos en la documentación de Gatsby como guías o tutoriales, ya que pueden ser encontrados en una sección con contenido relacionado y no enterrados entre post de blog paginados.
- **Contenido promocional.** Por favor no envíes contenido al blog de Gatsby con el único proposito de promocionar un producto, a ti o crear una red.
  - **Aquí esta lo que puedes hacer en su lugarL** Sí tienes un producto o un proyecto que quieres compartir en el blog de Gatsby, enfócate en información práctica, y asegúrate de que hay una relación clara con Gatsby o temas relacionados con Gatsby. Puedes escribir una guía paso a paso para usar tu producto con Gatsby. Puedes escribir un caso de estudio que resalte el impacto directo que Gatsby ha tenido en tu asombroso proyecto y ofrecer consejos útiles a otros para recrear tu éxito.
- **Contenido que parece no tener un beneficio claro para los usuarios de Gatsby y/o su comunidad.** Por ejemplo, sí estás escribiendo sobre un caso de uso o integración que es extremadamente de nicho o única para condiciones en específico que son realmente poco comúnes en tu organización, el blog de Gatsby puede no ser el mejor lugar para tu contenido. De igual forma, sí tu post del blog no tiene relación directa con Gatsby (o una interesante relación indirecta con Gatsby), entonces puede ser apropiado para un blog personal u otro blog de la comunidad.

**Por favor ten en cuenta** que estas son pautas, no reglas. Sí piensas que tu post del blog pertenece al blog de Gatsby, te recomendamos enviarlo. Mientras que nos reservamos el derecho a decidir que es apropiado o no para el blog de Gatsby, también valoramos y aplaudimos tu creatividad y contribuciones.

## Realizar cambios en el sitio web

Si quieres realizar cambios, mejoras, o añadir nueva funcionalidad al sitio web, no necesitas configurar por completo el repositorio de Gatsby para contribuir. Puedes activar tu propia instancia del sitio web de Gatsby con estos pasos:

- Clona [el repositorio de Gatsby](https://github.com/gatsbyjs/gatsby/) y navega a `/www`.
- Ejecuta `yarn` para instalar todas las dependencias del sitio web.
- Ejecuta `npm run develop` para previsualizar el sitio en `http://localhost:8000/`.

> Nota: Si estás experimentando problemas en un equipo con Linux, ejecuta `sudo apt install libvips-dev`, para instalar una dependencia nativa. También puedes tomar como referencia la [guía de Gatsby en Linux](/docs/gatsby-on-linux/) para otros requerimientos específicos de Linux.

¡Ahora puedes hacer y previsualizar tus cambios antes de lanzar un pull request!

Para instrucciones para configurar el repositorio por completo, visita la página de [contribuciones de código](/contributing/code-contributions/).
