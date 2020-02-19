---
title: Auditar con Lighthouse
---

Citando el [sitio web de Lighthouse](https://developers.google.com/web/tools/lighthouse/):

> Lighthouse es una herramienta automatizada de código abierto diseñada para mejorar la calidad de las páginas webs. Puedes ejecutarla en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas (_PWAs_), y más.

Lighthouse está incluida en las herramientas de desarrollo de Chrome. Ejecutar su auditoría -- y luego abordar los errores que encuentra e implementar las mejoras que sugiere -- es una excelente manera de preparar tu sitio para ponerlo online. Te ayuda a confiar en que tu sitio es lo más rápido y accesible posible.

Si aún no lo has hecho, necesitas crear una compilación de producción de tu sitio Gatsby. El servidor de desarrollo de Gatsby está optimizado para que el desarrollo sea rápido, pero el sitio que genera, aunque se parece mucho a una versión de producción del sitio, no está tan optimizado.

### Crear una compilación de producción

1.  Detén el servidor de desarrollo (si todavía se está ejecutando) y ejecuta:

```shell
gatsby build
```

> 💡 Esto crea una compilación de producción de tu sitio y genera los archivos estáticos compilados en el directorio `public`.

2.  Mira el sitio de producción localmente. Ejecuta:

```shell
gatsby serve
```

<<<<<<< HEAD
Una vez que inicie, puedes ver tu sitio en `localhost:9000`.
=======
Once this starts, you can now view your site at `http://localhost:9000`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

### Ejecuta una auditoría con Lighthouse

Ahora ejecutemos tu primera prueba con Lighthouse.

1.  Abre el sitio en Chrome (si aún no lo hiciste) y luego abre las herramientas de desarrollo (_Chrome DevTools_).

2.  Haz clic en la pestaña "Auditorías" donde verás una pantalla como la siguiente:

![Iniciar auditoría con Lighthouse](./images/lighthouse-audit.png)

3.  Haz clic en "Ejecutar una auditoria..." (Todos los tipos de auditoría disponibles deben seleccionarse de manera predeterminada). Luego haz clic en "Ejecutar auditoría". (Tomará aproximadamente un minuto en ejecutar la auditoría). Una vez que se complete la auditoría, deberías ver resultados como estos:

![Resultados de auditoría con Lighthouse](./images/lighthouse-audit-results.png)

Como puedes ver, el rendimiento de Gatsby es excelente por defecto pero nos faltan algunas cosas para _PWA_, Accesibilidad, Mejores Prácticas y SEO que mejorarán nuestra puntuación (y en el proceso harán que tu sitio sea mucho más amigable para los visitantes y los motores de búsqueda). Para mejorar aún más tus puntuaciones, consulta los enlaces en "Siguientes pasos" a continuación.

Siguientes pasos:

- [Agregar un archivo de manifiesto](/docs/add-a-manifest-file/)
- [Agregar soporte fuera de línea](/docs/add-offline-support/)
- [Agregar metadatos de página](/docs/add-page-metadata/)
