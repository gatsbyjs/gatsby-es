---
title: Estructura de un proyecto Gatsby
---

Dentro de un proyecto Gatsby, quizás mires algunas o todas las carpetas y archivos siguientes:

```
/
|-- /.cache
|-- /plugins
|-- /public
|-- /src
    |-- /pages
    |-- /templates
    |-- html.js
|-- /static
|-- gatsby-config.js
|-- gatsby-node.js
|-- gatsby-ssr.js
|-- gatsby-browser.js
```

### Carpetas

- **`/.cache`** _Generada automáticamente._ Esta carpeta es una cache interna creada automáticamente por Gatsby. Los archivos dentro de esta carpeta no deben ser modificados. Debe ser agregada al archivo `.gitignore` si aún no está.

- **`/public`** _Generada automáticamente._ El resultado del proceso de compilación se pondrá dentro de esta carpeta. Debe ser agregada al archivo `.gitignore` si aún no está.

- **`/plugins`** Esta carpeta hospeda plugins ("locales") específicos del proyecto que no son publicados como un paquete `npm`. Revisa la [documentación de plugin](/docs/plugins/) para más detalles.

- **`/src`** Este directorio contendrá todo el código relacionado con el frontend que verás en tu página (lo que ves en el navegador), como la cabecera de tu sitio, o una plantilla de página. “Src” es una convención para “source code” (código fuente).

  - **`/pages`** Los componentes dentro de src/pages se vuelven páginas automáticamente con rutas basadas en el nombre del archivo. Revisa la [documentación de páginas](/docs/recipes/#creating-pages) para más detalles.
  - **`/templates`** Contienen plantillas para crear páginas de manera programática. Revisa la [documentación de plantillas](/docs/building-with-components/#page-template-components) para más detalles.
  - **`html.js`** Para una configuración personalizada por defecto .cache/default_html.js. Revisa la [documentación de html personalizado](/docs/custom-html/) para más detalles.

- **`/static`** Si pones un archivo dentro de la carpeta static, no será procesado por Webpack. En vez de eso será copiado dentro de la carpeta public sin ser tocado. Revisa la [documentación de activos](/docs/static-folder/#adding-assets-outside-of-the-module-system) para más detalles.

### Archivos

- **`gatsby-browser.js`**: Este archivo es donde Gatsby espera encontrar cualquier uso de [la API de Gatsby navegador](/docs/browser-apis/) (si alguno). Esto permite la personalización/extensión de las configuraciones por defecto de Gatsby que afectan al navegador.

- **`gatsby-config.js`**: Este es el archivo principal de configuración de un sitio Gatsby. Aquí es donde puedes especificar la información acerca de tu sitio (metadatos) como el título y descripción del sitio, cuales plugins de Gatsby te gustaría incluir, etc. Revisa la [documentación de configuración](/docs/gatsby-config/) para más detalles.

- **`gatsby-node.js`**: Este archivo es donde Gatsby espera encontrar cualquier uso de la [API de Gatsby node](/docs/node-apis/) (si alguno). Esto permite la personalización/extensión de las configuraciones por defecto de Gatsby que afectan las piezas del proceso de compilado del sitio.

- **`gatsby-ssr.js`**: Este archivo es donde Gatsby espera encontrar cualquier uso de la [API Gatsby renderizado del lado del servidor](/docs/ssr-apis/) (si alguno). Esto permite la personalización de las configuraciones por defecto de Gatsby que afectan el renderizado del lado del servidor.

### Miscelanea:

La estructura archivo/carpeta descrita anteriormente refleja los archivos y carpetas específicos de Gatsby. Puesto que los sitios Gatsby también son aplicaciones React, es común el utilizar patrones de organización de código estándar, como carpetas `/components` y `/utils` dentro de `/src`. La [documentación de React](https://reactjs.org/docs/faq-structure.html) contiene más información de una estructura de carpetas típica en una aplicación React.