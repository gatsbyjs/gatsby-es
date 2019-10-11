---
El titulo: Cómo etiquetar un issue
---

## ¿Qué son las etiquetas de issue?

Las etiquetas de issue son una herramienta de GitHub que se utilizan para agrupar issues en una o varias categorías.

[Echa un vistazo a las etiquetas de Gatsby (y sus descripciones)](https://github.com/gatsbyjs/gatsby/issues/labels)

## ¿Por qué etiquetar issues?

Gatsby es un proyecto muy activo con muchos nuevos issues abiertos cada día. Las etiquetas de issues ayudan identificando:

- issues buenos para que los nuevos contribuidores trabajen en ellos
- errores reportados y confirmados
- solicitudes de funcionalidades
- issues duplicados
- issues que están parados o bloqueados

## ¿Quién puede etiquetar issues?

Cualquier persona que sea miembro del [equipo de mantenedores de Gatsby](https://github.com/orgs/gatsbyjs/teams/maintainers) puede etiquetar issues.

Puedes obtener una invitación para el equipo por tener un pull request que fue incluido en el proyecto de Gatsby. Comprueba la lista de issues ['help wanted'] (https://github.com/gatsbyjs/gatsby/labels/%F0%9F%93%8D%20status%3A%20help%20wanted) y [la guía de cómo contribuir](/contributing/how-to-contribute/) para empezar.

**NOTA:** Si ya tienes un pull request incluido y _no_ has sido invitado al equipo mantenedores, por favor ve a [la página de la tienda](https://store.gatsbyjs.org/) y solicita un código de descuento. ¡Deberías obtener una invitación al equipo — _y conseguir swag de Gatsby gratis!_ Si esto no funciona, por favor envía un correo electrónico a team@gatsbyjs.com y te invitaremos.

## Cómo etiquetar un issue

Idealmente, cada issue debería tener una etiqueta `type:` aplicada a el. Opcionalmente una etiqueta `status:` u otras etiquetas también pueden ser aplicadas.

Antes de seguir, hazte familiar con [las etiquetas de los issues de Gatsby y sus descripciones](https://github.com/gatsbyjs/gatsby/issues/labels).

Los amplios pasos para etiquetar un issue son:

- Leer un issue
- Elegir las etiquetas que se aplican a ese issue
- Eso es todo - siéntate y relájate, tal vez tome unos momentos para disfrutar de la satisfacción de un trabajo bien hecho

El resto de este documento describirá cómo elegir las etiquetas correctas para un issue.

### Encontrar un issue que te interesa

Comienza con [la lista de issues de Gatsby](https://github.com/gatsbyjs/gatsby/issues) y haz scroll a través de esta hasta que veas uno reciente que despierte tu interés. Alternativamente, puedes ver la [lista de unlabelled issues](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aopen+is%3Aissue+no%3Alabel).

### Leer un issue

Lee el issue y cualquier comentario para entender de qué se trata el issue.

### Elige una etiqueta `type:`

Elige una etiqueta de tipo en el menú desplegable de etiquetas, en el lado derecho del issue.

![Dropdown de etiquetas de GitHub](./images/github-label-list.png)

Puedes comprobar a través de las [descripciones de etiquetas](https://github.com/gatsbyjs/gatsby/issues/labels) para obtener más información sobre cada una de ellas.

El tipo más común de los issues es `type: question or discussion`, típicamente puedes aplicar esto a issues que son sin límites determinados o no tienen ningún paso siguiente claro.

Está bien cambiar el tipo de un issue ya que más información se hace disponible. Lo que empieza como `type: question or discussion`, puede que más tarde necesite ser cambiado a `type: bug`.

El cambio de etiquetas es rápido y fácilmente reversible, así que no te preocupes demasiado de la aplicación de una etiqueta "incorrecta".

Elige una etiqueta `type:` apropiada y estarás listo para ir al siguiente paso.

### Elija un `status:` etiqueta (opcional)

Compruebe a través de la [`status:` etiquetas (y sus descripciones)](https://github.com/gatsbyjs/gatsby/issues/labels), si alguno se aplica a este de la issue agregarlos como sea necesario.

Ejemplos de aplicación de etiquetas `status:` podrían ser:

- Un issue que depende de una dependencia externa cambiada podría ser marcada por 'el estado: bloqueado' `status: blocked`

- Un issue con una descripción clara de cómo puede ser resuelto podría ser marcada `status: help wanted`.

- Un issue esto pierde la información requerida ayudar al autor podría ser marcada por `status: needs more info`

- Un issue que describe un error de programación sin pasos claros para reproducirse podría ser marcada por `status: needs reproduction`

- Un issue que describe un error de programación donde hay pasos para reproducir el error de programación y ha dirigido el código en la localidad y ha visto que el error usted mismo puede ser marcado `status: confirmed`

### Elija cualquier otra etiqueta

Hay unas otras etiquetas que pueden ser a veces aplicadas a un issue. Aquí están algunos ejemplos más de cuando usarlos:

- `good first issue` puede ser usada cuando un issue es un trabajo pequeño, claramente definido que podría ser completado por alguien sin conocimiento a fondo de Gatsby y cómo trabaja. Estos issues son particularmente convenientes para la gente que hace sus primeras contribuciones a código abierto.

- `stale?` puede ser usado en un issue donde el autor no ha contestado a peticiones de más información en al menos 20 días.

### El final

¡Y has acabado! Puedes dejarlo por hoy o volver al primer paso para poner una etiqueta a otro issue.

## La conclusión

El etiquetaje a issues es una gran manera de ayudar en el proyecto de Gatsby sin tener en cuenta tu nivel de experiencia.
