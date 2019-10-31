---
title: Respuestas a preguntas sobre TI y seguridad
---

En grandes compañías, como la de Fortune 500, operan equipos de seguridad que auditan las nuevas tecnologías que se estén incorporando a la compañía.

Aquí puedes encontrar algunos puntos de referencia que te podrían ayudar a responder a algunas preguntas que los ingenieros de seguridad te hagan en caso que estén interesados en tu proyecto:

- Dado que Gatsby compila tu sitio en archivos planos, en lugar de tener que ejecutar servidores y bases de datos a las que se dirigen los usuarios, se reduce la superficie de ataque del sitio frente a intrusos.
- Gatsby agrega una capa de indirección que esconde tu CMS -- por lo que incluso si tu CMS _es_ vulnerable, los agentes malintencionados no tendrán idea de dónde encontrarlo. Esto contrasta con otros sistemas en los que los agentes malintencionados pueden localizar fácilmente el panel de control de administración en, por ejemplo, `/wp-admin` e intentar hackearlo.
- Gatsby te permite servir tu sitio Web a través de una CDN global, sin importar qué CDN esté utilizando tu empresa (por ejemplo, Akamai, Cloudflare, Fastly...), lo que elimina eficazmente el riesgo de ataques DDOS.

Es útil recalcar al personal de seguridad que estos beneficios fueron factores que motivaron a que se seleccionara a Gatsby para el proyecto. Has escogido a Gatsby, en parte, porque es _más_ seguro.

Más información sobre la seguridad en Gatsby: [https://www.gatsbyjs.org/blog/2019-04-06-security-for-modern-web-frameworks/](/blog/2019-04-06-security-for-modern-web-frameworks/)

--

**Nota:** ¿Tienes ideas adicionales sobre cómo contestar preguntas sobre TI y seguridad relacionadas con los proyectos Gatsby? Aceptamos con gusto contribuciones a las documentaciones de Gatsby. Descubre [cómo contribuir](/contributing/docs-contributions/).
