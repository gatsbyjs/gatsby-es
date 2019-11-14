---
title: Estilos en Ámbito de Componentes con Módulos CSS
---

CSS en ámbito de componentes te permite escribir CSS tradicional y portátil con efectos secundarios mínimos: no tendrás que preocuparte por conflictos de nombres de selectores o por afectar los estilos de otros componentes.

Gatsby trabaja sin ninguna configuración requerida con [módulos CSS](https://github.com/css-modules/css-modules), una solución popular para escribir CSS en ámbito de componentes. Aquí tenemos un [ejemplo de un sitio que usa módulos CSS](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-css-modules).

## ¿Qué es un módulo CSS?

Citando a [la página de inicio de Módulos CSS](https://github.com/css-modules/css-modules):

> Un **módulo CSS** es un archivo CSS, en el cual, todos los nombres de clases y animaciones están scoped localmente, por defecto.

Los módulos CSS te permiten escribir estilos en archivos CSS, utilizándolos como objetos JavaScript para procesamiento y seguridad adicionales. Los módulos CSS son muy populares porque, automáticamente, hacen que los nombres de clases y animaciones sean únicos para que no haya que preocuparse por conflictos de nombres de selectores.

### Ejemplo de un módulo CSS

El contenido de un módulo CSS no es diferente al CSS normal, pero la extensión del archivo es diferente para marcar que el archivo será procesado.

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

```jsx:title=src/components/container.js
import React from "react"
// highlight-next-line
import containerStyles from "./container.module.css"

export default ({ children }) => (
  // highlight-next-line
  <section className={containerStyles.container}>{children}</section>
)
```

En este ejemplo, se importa un módulo CSS y se declara como un objeto JavaScript llamado `containerStyles`. Luego, una clase CSS de ese objeto se referencia en el atributo `className` de JSX mediante `containerStyles.container`, el cual se renderiza a HTML con nombres de clases CSS dinámicos, como `container-module--container--3MbgH`.

### Habilitar hojas de estilo de usuario con un nombre de clase estable

Agregar un `className` de CSS persistente a tu marcado JSX junto con el código de tus módulos CSS puede facilitarle a los usuarios tomar ventaja de las [Hojas de estilo de usuario](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para accesibilidad.

Aquí tenemos un ejemplo donde el nombre de clase `container` se agrega al DOM junto con los nombres de clases del módulo, creados dinámicamente:

```jsx:title=src/components/container.js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <section className={`container ${containerStyles.container}`}>
    {children}
  </section>
)
```

Un usuario del sitio podría escribir, más tarde, sus propios estilos CSS que coincidan con los elementos HTML con un nombre de clase `.container`, y no se verían afectados si llegara a cambiar el nombre o la ruta del módulo CSS.

## ¿Cuándo usar módulos CSS?

Los módulos CSS son muy recomendables para quienes están iniciando en crear con Gatsby (y React en general) ya que les permite escribir archivos CSS portátiles y regulares mientras obtienen beneficios de rendimiento como solo agrupar código referenciado.

## ¿Cómo construr una página usando Módulos CSS?

Visita la [sección Módulos CSS del tutorial](/tutorial/part-two/#css-modules) para un recorrido guiado sobre cómo construir una página con Módulos CSS.
