---
title: Construyendo con Componentes
---

Para usar Gatsby, necesitarás un conocimiento básico sobre componentes en React.

El [tutorial oficial](https://reactjs.org/tutorial/tutorial.html)
es un buen lugar para empezar.

## ¿Por qué componentes en React?

La arquitectura de componentes de React simplifica la construcción de sitios web grandes incentivando la
modularidad, la reusabilidad, y las abstracciones claras. React tiene un gran ecosistema de
componentes de código abierto, tutoriales, y herramientas que pueden ser usadas sin problemas para
construir sitios con Gatsby. Gatsby está construido para comportarse casi exactamente como una
aplicación React normal.

El siguiente modelo muestra cómo datos de un origen pueden ser consultados por GraphQL para usarlos dentro de componentes en el proceso de construcción de un sitio con Gatsby:

<LayerModel initialLayer="View" />

[Pensando en React](https://facebook.github.io/react/docs/thinking-in-react.html)
es un buen recurso para aprender cómo estructurar aplicaciones con React.

## ¿Cómo usa Gatsby componentes React?

Todo en Gatsby está construido usando componentes.

Una estructura de directorios básica de un proyecto podría verse así:

```text
.
├── gatsby-config.js
├── package.json
└── src
    ├── html.jsx
    ├── pages
    │   ├── index.jsx
    │   └── posts
    │       ├── 01-01-2017
    │       │   └── index.md
    │       ├── 01-02-2017
    │       │   └── index.md
    │       └── 01-03-2017
    │           └── index.md
    ├── templates
        └── post.jsx
```

### Componentes de página

Los componentes dentro de `src/pages` se convierten en páginas automáticamente con rutas basadas en
su nombre de archivo. Por ejemplo `src/pages/index.jsx` se asigna a `yoursite.com`
y `src/pages/about.jsx` se convierte en `yoursite.com/about/`. Todos los archivos `.js` o `.jsx`
en el directorio _pages_ deben resolver en una cadena de texto o en un componente React,
de lo contrario el _compilado_ fallará.

Ejemplo:

```jsx:title=src/pages/about.jsx
import React from "react";

function AboutPage(props) {
  return (
    <div className="about-container">
      <p>Acerca de mi.</p>
    </div>
  );
}

export default AboutPage;
```

### Componentes de plantilla de página

Puedes crear páginas mediante programación usando "componentes de plantilla de página". Todas
las páginas son componentes React pero muy a menudo estos componentes son solo _envoltorios_ para datos desde archivos u otros orígenes.

`src/templates/post.jsx` es un ejemplo de un componente de página. Consulta a GraphQL
por datos _markdown_ y entonces renderiza la página usando estos datos.

Mira la [parte siete](/tutorial/part-seven/) del tutorial para una introducción
detallada de crear páginas mediante programación.

Ejemplo:

```jsx:title=src/templates/post.jsx
import React from "react";
import { graphql } from "gatsby";

function BlogPostTemplate(props) {
  const post = props.data.markdownRemark;
  return (
    <div>
      <h1>{post.frontmatter.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.html }} />
    </div>
  );
}

export default BlogPostTemplate;

export const pageQuery = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`;
```

### Componente HTML

`src/html.jsx` es responsable de todo lo que no sea donde Gatsby está en
el `<body />`.

En este archivo, puedes modificar los metadatos del `<head>` y la estructura general del
documento y añadir enlaces externos.

Por lo general, debes omitir esto en tu sitio, ya que el archivo html.js predeterminado será
suficiente. Si necesitas más control sobre el renderizado en el servidor, entonces es importante
tener un html.js.

Ejemplo:

```jsx:title=src/html.jsx
import React from "react";
import favicon from "./favicon.png";

let inlinedStyles = "";
if (process.env.NODE_ENV === "production") {
  try {
    inlinedStyles = require("!raw-loader!../public/styles.css");
  } catch (e) {
    console.log(e);
  }
}

function HTML(props) {
  let css;
  if (process.env.NODE_ENV === "production") {
    css = (
      <style
        id="gatsby-inlined-css"
        dangerouslySetInnerHTML={{ __html: inlinedStyles }}
      />
    );
  }
  return (
    <html lang="en">
      <head>
        <meta charSet="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        {props.headComponents}
        <link rel="shortcut icon" href={favicon} />
        {css}
      </head>
      <body>
        <div id="___gatsby" dangerouslySetInnerHTML={{ __html: props.body }} />
        {props.postBodyComponents}
      </body>
    </html>
  );
}
```

Estos son ejemplos de las diferentes formas en que los componentes React son usados en sitios Gatsby.
Para ver ejemplos completos, consulta el
[directorio de ejemplos](https://github.com/gatsbyjs/gatsby/tree/master/examples) en
el repositorio de Gatsby.

### Componentes que no son de página

Un componente que no es de página es uno que está incrustado dentro de otro componente, formando una jerarquía de componente. Un ejemplo sería un componente _Header_ que está incluido en múltiples componentes de página.
Gatsby usa GraphQL para permitir a los componentes declarar los datos que necesiten. Usando el componente [StaticQuery](/docs/static-query/) o el [_hook_ useStaticQuery](/docs/use-static-query/), puedes colocar un componente que no sea de página con sus datos.
