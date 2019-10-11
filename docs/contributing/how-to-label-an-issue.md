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

**NOTA:** Si ha hecho combinar ya una solicitud de tirón y _no_ ha sido invitado al equipo maintainers, por favor vaya a [el tablero de instrumentos](https://store.gatsbyjs.org/) y solicite un código de descuento.¡Debería conseguir invitar al equipo — _y consigue el botín de Gatsby libre!_ Si esto no trabaja, por favor correo electrónico team-gatsbyjs.com y le invitaremos.

## Cómo etiquetar un issue

Idealmente, cada issue debería tener un `type:` solo la etiqueta se aplicó a ello. Opcionalmente un `status:` a etiqueta u otras etiquetas también pueden ser aplicadas.

Antes de seguir, hágase familiar con [las etiquetas de la issue de Gatsby y sus descripciones](https://github.com/gatsbyjs/gatsby/issues/labels).

Los amplios pasos al etiquetaje una issue son:

- Leer un issue
- Elija las etiquetas que se aplican a ese issue
- Eso es todo - siéntate y relájate, tal vez tome unos momentos para disfrutar de la satisfacción de un trabajo bien hecho

El resto de este documento describirá cómo elegir las etiquetas correctas para un issue.

### Encontrar un issue que le interesa

Comience con [la lista de issues de Gatsby](https://github.com/gatsbyjs/gatsby/issues) y voluta a través de hasta que vea uno reciente que golpea su interés. Alternativamente, puede ver la [lista de unlabelled issues](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aopen+is%3Aissue+no%3Alabel).

### Leer un issue

Lea el issue y cualquier comentario para entender de qué se trata el issue.

### Elija un `type:` etiqueta

Elija una etiqueta de tipo en el menú desplegable de etiquetas, en el lado derecho del issue.

![GitHub etiqueta dropdown](./images/github-label-list.png)

Puede comprobar a través de las [descripciones de etiquetas](https://github.com/gatsbyjs/gatsby/issues/labels) para obtener más información sobre cada uno de ellos.

El tipo más común de la issues es `type: la pregunta o la discusión`, típicamente puede aplicar esto a issues que son sin límites determinados o tienen ningún siguiente paso claro.

Está bien para cambiar el tipo de una issue ya que más información se hace disponible. Que ventajas como `type: la pregunta o la discusión`, tendrían que más tarde ser cambiadas a `type: error de programación`.

El cambio de etiquetas es rápido y fácilmente reversible, así no se preocupe demasiado de la aplicación de una etiqueta "incorrecta".

Elija un `type:` apropiado: la etiqueta y usted están listos para circular al siguiente paso.

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

- `la primera issue buena` puede ser usada cuando un issue es un trabajo pequeño, claramente definido que podría ser completado por alguien sin el conocimiento a fondo de Gatsby y cómo trabaja. Estas issues son particularmente convenientes para la gente que hace sus primeras contribuciones de la fuente abiertas.

- `stale?` puede ser usado en un issue donde el autor no ha contestado a peticiones de más información en al menos 20 días

### El final

¡Y es hecho! Lo puede llamar un día o volver al primer paso para poner etiqueta a otra issue.

## La conclusión

El etiquetaje a issues es una gran manera echar una mano en el proyecto de Gatsby sin tener en cuenta su nivel de experiencia.
