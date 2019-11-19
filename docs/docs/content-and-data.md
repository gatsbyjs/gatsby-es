---
title: Abastecimiento de contenido y datos
---

Una característica central de Gatsby es su capacidad para **cargar datos desde cualquier lugar**. Esto es parte de lo que hace que Gatsby sea más poderoso que los generadores de sitios estáticos que se limitan a cargar solo contenido de archivos Markdown.

Un beneficio principal de este enfoque de "datos desde cualquier lugar" es que permite a los equipos administrar su contenido en casi cualquier [backend](/docs/glossary/#backend) que prefieran.

Gatsby usa plugins de origen para obtener datos. [Ya existen numerosos plugins de origen](/plugins/?=gatsby-source) para extraer datos de otras API, CMS y bases de datos. Cada plugin obtiene datos de su fuente, lo que significa que el plugin fuente del sistema de archivos sabe cómo obtener datos del sistema de archivos, el plugin de WordPress sabe cómo obtener datos de la API de WordPress, etc. Al incluir múltiples complementos de origen, puedes obtener datos y combinarlos todos en una capa de datos.

Bonus: lee sobre [Temas de Gatsby y documentos distribuidos](/blog/2019-07-03-using-themes-for-distributed-docs/) trabajando bien juntos en el blog de Gatsby.

_(Si aún no hay un plugin para tu opción favorita, ¡considera [contribuir](/docs/creating-plugins) con uno!)_

<GuideList slug={props.slug} />
