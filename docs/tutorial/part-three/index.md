---
title: Creando componentes layout anidados
typora-copy-images-to: ./
disableTableOfContents: true
---

¡Bienvenido a la parte tres!

## ¿Qué hay en este tutorial?

En esta parte aprenderás acerca de los plugins de gatsby y a cómo crear componentes "_layout_".

Los plugins de Gatsby son paquetes de JavaScript que ayudan a añadir funcionalidades a un sitio web de Gatsby. Gatsby está diseñado para ser extensible, lo que significa que sus plugins son capaces de extender y modificar todo lo que hace.

Los componentes _layout_ son para secciones de tu sitio web que quieras compartir entre varias páginas. Por ejemplo, los sitios web tendrán comúnmente un componente _layout_ que tendrá una cabecera y un pie de página. Otra cosa común para añadir a tus componentes _layouts_ son una barra lateral y/o un menú de navegación. En esta página, por ejemplo, la cabecera en la parte de arriba es parte del componente _layout_ de gatsbyjs.org.

Sumerjámonos en la parte tres.

## Usando los plugins

Probablemente estés familiarizado con la idea de los plugins. Muchos sistemas de software permiten la adición de plugins personalizados para añadir nuevas funcionalidades o incluso modificar el núcleo del software. Los plugins de Gatsby funcionan de la misma manera.

Los miembros de la comunidad (¡como tú!) pueden contribuir con plugins (pequeñas cantidades de código JavaScript) que otros pueden usar cuando estén construyendo sitios web con Gatsby.

> ¡Ya hay cientos de plugins! Esplora la [librería de plugins](/plugins/) de Gatsby.

Nuestro objetivo con los plugins es hacerlos fáciles de instalar y usar. Posiblemente estarás usando plugins en casi todos los sitios web Gatsby que construyas. Mientras trabajas en el resto del tutorial tendrás muchas oportunidades para practicar instalando y usando plugins.

Para una introducción inicial al uso de los plugins, instalaremos e implementaremos el plugin de Gatsby para Typography.js.

[Typography.js](https://kyleamathews.github.io/typography.js/) es una librería de JavaScript que genera estilos globales básicos para la tipografía de tus sitios web. La librería tiene su [respectivo plugin de Gatsby](/packages/gatsby-plugin-typography/) para optimizar su uso en un sitio web Gatsby.

### ✋ Crea un nuevo sitio web Gatsby

Como hemos mencionado en la [parte dos](/tutorial/part-two/), en este punto es probablemente una buena idea cerrar la(s) ventana(s) de terminal y archivos de proyecto de las partes anteriores de este tutorial, para mantener las cosas limpias en tu escritorio. Luego abre una nueva ventana de terminal y ejecuta el siguiente comando para crear un nuevo sitio web Gatsby en un directorio llamado `tutorial-parte-tres` y entonces muévete a este nuevo directorio:

```shell
gatsby new tutorial-parte-tres https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-parte-tres
```

### ✋ Instalar y configurar `gatsby-plugin-typography`

Hay dos pasos principales para usar un plugin: Instalación y configuración.

1. Instala el paquete de NPM `gatsby-plugin-typography`

```shell
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> Nota: Typography.js requiere unos pocos paquetes adicionales, así que esos están incluidos en las instrucciones. Requisitos adicionales como este estarán en las instrucciones de "instalación" de cada plugin.

2. Edita el archivo `gatsby-config.js` en la raíz de tu proyecto con lo siguiente:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

El `gatsby-config.js` es un fichero especial que Gatsby reconocerá automáticamente. Aquí es donde añades plugins y otras configuraciones de sitio web.

> Mira la [documentación sobre gatsby-config.js](/docs/gatsby-config/) para saber más, si quieres.

3. Typography.js necesita un fichero de configuración. Crea un nuevo directorio llamado `utils` en el directorio `src`. Después añade un nuevo fichero llamado `typography.js` en `utils` y copia lo siguiente en el fichero:

```javascript:title=src/utils/typography.js
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

4. Inicia el servidor de desarrollo.

```shell
gatsby develop
```

Una vez que el sitio web cargue, si inspeccionas el HTML generado usando la herramienta de desarrollo de Chrome, verás que el plugin añade un elemento `<style>` en el elemento `<head>` con su CSS generado:

![typography-styles](typography-styles.png)

### ✋ Crea algún conetenido y cambia los estilos

Copia lo siguiente en `src/pages/index.js` para que puedas ver mejor el efecto del CSS generado por Typography.js.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div>
    <h1>¡Hola! ¡Estoy construyendo un Gatsby falso como parte de un tutorial!</h1>
    <p>
      ¿Que qué me gusta hacer? Muchas cosas, por supuesto, pero definitivamente disfruto construyendo sitios web.
    </p>
  </div>
)
```

Tu sitio web debería verse de esta forma:

![no-layout](no-layout.png)

Hagamos una mejora rápida. Muchos sitios tienen una única columna de texto centrada en el medio de la página. Para crear esto, añade los siguientes estilos al `<div>` en `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  // highlight-next-line
  <div style={{ margin: `3rem auto`, maxWidth: 600 }}>
    <h1>¡Hola! ¡Estoy construyendo un Gatsby falso como parte de un tutorial!</h1>
    <p>
      ¿Que qué me gusta hacer? Muchas cosas, por supuesto, pero definitivamente disfruto construyendo sitios web.
    </p>
  </div>
)
```

![with-layout2](with-layout2.png)

Genial. ¡Has instalado y configurado tu primer plugin de Gatsby!

## Creando componentes _layout_

Ahora vamos a aprender acerca de los componentes _layout_. Para prepararnos para esta parte, añade unas pocas páginas nuevas a tu proyecto: una página "acerca de" y una página de contacto.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div>
    <h1>Sobre mí</h1>
    <p>Soy lo suficientemente bueno, lo suficientemente inteligente y, vaya que sí, ¡le gusto a la gente!</p>
  </div>
)
```

```jsx:title=src/pages/contact.js
import React from "react"

export default () => (
  <div>
    <h1>¡Me encantaría hablar! Envíame un email a la dirección de abajo</h1>
    <p>
      <a href="mailto:me@example.com">me@example.com</a>
    </p>
  </div>
)
```

Veamos cómo luce nuestra página de "acerca de":

![about-uncentered](about-uncentered.png)

Mmm. Sería mejor si el contenido de las dos nuevas páginas estuviera centrado como en la página principal. Y sería mejor aún tener algún tipo de navegación global para que sea más fácil para los visitantes encontrar y visitar cada una de las subpáginas.

Abordarás estos cambios creando tu primer componente _layout_.

### ✋ Crea tu primer componente _layout_

1. Crea un nuevo directorio en `src/components`.

2. Crea un component _layout_ muy básico en `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

3. Importa este nuevo componente _layout_ en tu componente página `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>¡Hola! ¡Estoy construyendo un Gatsby falso como parte de un tutorial!</h1>
    <p>
      ¿Que qué me gusta hacer? Muchos cosas, por supuesto, pero definitivamente disfruto construyendo sitios web.
    </p>
  </Layout> {/* highlight-line */}
)
```

![with-layout2](with-layout2.png)

¡Genial, el componente _layout_ está funcionando! El contenido de tu página de inicio sigue centrada.

Pero intenta navegar a `/about/` o a `/contact/`. El contenido en esas páginas no estará centrado.

4. Importa el componente _layout_ en `about.js` y en `contact.js` (como has hecho con `index.js` en los pasos anteriores).

¡El contenido de tus tres páginas está centrado gracias a este solo componente _layout_ compartido!

### ✋ Añade un título al sitio web

1. Añade la siguiente línea a tu nuevo componente _layout_:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MiSitioWebGenial</h3> {/* highlight-line */}
    {children}
  </div>
)
```

Si vas a alguna de tus tres páginas, verás el mismo título añadido, por ejemplo, en la página `/about/`:

![with-title](with-title.png)

### ✋ Añade enlaces de navegación entre las páginas

1. Copia lo siguiente en tu fichero del componente _layout_:

```jsx:title=src/components/layout.js
import React from "react"
// highlight-start
import { Link } from "gatsby"

const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)
// highlight-end

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {/* highlight-start */}
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MiSitioWebGenial</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Inicio</ListLink>
        <ListLink to="/about/">Acerca de</ListLink>
        <ListLink to="/contact/">Contacto</ListLink>
      </ul>
    </header>
    {/* highlight-end */}
    {children}
  </div>
)
```

![with-navigation2](with-navigation.png)

¡Y ahí lo tienes! Un sitio web con tres páginas y una navegación global básica.

_Reto:_ Con tus nuevos poderes de "componente _layout_", ¡intenta añadir cabeceras, pies de páginas, navegaciones globales, barras laterales, etc. a tus sitios web Gatsby!

## ¿Qué viene luego?

¡Continúa en la [parte cuatro del tutorial](/tutorial/part-four/) donde aprenderás acerca de la capa de datos de Gatsby y a crear páginas de forma automática!
