---
title: Componentes de diseño
---

En esta guía, aprenderá el enfoque de Gatsby para los diseños, cómo crear y usar componentes de diseño y cómo evitar que los componentes de diseño se desmonten.

### El enfoque de Gatsby a los diseños

Gatsby no aplica automáticamente de manera predeterminada, diseños a las páginas (sin embargo, hay formas de hacerlo lo cual se tratarán en una sección posterior). En cambio, Gatsby sigue el modelo compositivo de React para importar y usar componentes. Esto hace posible crear múltiples niveles de diseños, p. ej. un encabezado y pie de página global, y luego en algunas páginas, un menú de barra lateral. También facilita el paso de datos entre el diseño y los componentes de la página.

### ¿Qué son los componentes de diseño?

Los componentes de diseño son para secciones de su sitio que desea compartir en varias páginas. Por ejemplo, los sitios de Gatsby comúnmente tendrán un componente de diseño con un encabezado y pie de página compartidos. Otras cosas comunes para agregar a los diseños son una barra lateral y / o un menú de navegación. En esta página, por ejemplo, el encabezado en la parte superior es parte del componente de diseño de gatsbyjs.org.

### Cómo crear componentes de diseño

Se recomienda crear sus componentes de diseño junto con el resto de sus componentes. (p.ej. dentro `src/components/`).

Aquí hay un ejemplo de un componente de diseño muy básico en `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

### Cómo importar y agregar componentes de diseño a las páginas

Si desea aplicar un diseño a una página, deberá incluir el componente `Layout` que envuelva su página en él. Por ejemplo, así es como aplicaría su diseño a la página principal:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>Estoy en un diseño!</h1>
  </Layout> {/* highlight-line */}
)
```

Repita lo mismo para cada página y plantilla que necesita este diseño.

### Cómo evitar que los componentes de diseño se desmonten

Como se mencionó anteriormente, Gatsby, por defecto, no ajusta automáticamente las páginas en un componente de diseño. El componente de "nivel superior" es la página misma. Como resultado, cuando el componente de "nivel superior" cambia entre páginas, React volverá a representar a todos los elementos secundarios. Esto significa que los componentes compartidos como las navegaciones se desmontarán y volverán a montar. Esto interrumpirá las transiciones CSS o el estado React dentro de esos componentes compartidos.

Si necesita establecer un componente contenedor alrededor de los componentes de la página que no se desmontarán en los cambios de la página, use el **`wrapPageElement`** [browser API](/docs/browser-apis/#wrapPageElement) y el [SSR equivalent](/docs/ssr-apis/#wrapPageElement).

Alternativamente, puede evitar que su componente de diseño se desmonte utilizando [gatsby-plugin-layout](/packages/gatsby-plugin-layout/), que implementa las `wrapPageElement` APIs por usted.

### Otros recursos

- [Crear componentes de diseño anidados en Gatsby](/tutorial/part-three/)
- [La vida después de los diseños en Gatsby V2](/blog/2018-06-08-life-after-layouts/)
- [Migrar de v1 a v2](/docs/migrating-from-v1-to-v2/#remove-or-refactor-layout-components)
- [gatsby-plugin-layout](/packages/gatsby-plugin-layout/)
- [wrapPageElement Browser API](/docs/browser-apis/#wrapPageElement)
- [wrapPageElement SSR API](/docs/ssr-apis/#wrapPageElement)
