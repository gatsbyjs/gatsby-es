---
título: Usando múltiples temas juntos
---

## Que subre este tutorial

Este tutorial cubre como componer múltiples temas en un sitio final usando [gatsby-theme-blog](/packages/gatsby-theme-blog/), [gatsby-theme-notes](/packages/gatsby-theme-notes/) y [gatsby-mdx-embed](/packages/@pauliescanlon/gatsby-mdx-embed/) como ejemplos. También cubre el concepto de `component shadowing` con [Theme-UI](/docs/theme-ui/) para estilizado.

## Prerrequisitos

Este tutorial asume lo siguiente:

- Que entiendes los [fundamentos de Gatsby](/tutorial/#gatsby-fundamentals)
- Conocimiento sobre [temas de Gatsby](/docs/themes/what-are-gatsby-themes/)

## Repositorio de ejemplo

Puedes ver un [ejemplo completo funcionando de este tutorial](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-multiple-themes) en Github. Algunos trozos de código largos han sido editados por longitud y el código completo esta disponible para referencia en el repositorio de ejemplo.

## Crear un sitio nuevo

Usando el `starter` de `hello world`, crea un nuevo sitio y navega a ese directorio.

```shell
gatsby new multiple-themes https://github.com/gatsbyjs/gatsby-starter-hello-world
cd multiple-themes
```

## Instalar y componer los temas

Este paso compone [gatsby-theme-blog](/packages/gatsby-theme-blog/) y [gatsby-theme-notes](/packages/gatsby-theme-notes/).

1. Instala los temas:

```shell
npm install gatsby-theme-blog gatsby-theme-notes
```

2. Edita el archivo `gatsby-config.js` para agregar los temas al arreglo de plugins y para actualizar los metadatos del sitio:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `El titulo de tu sitio`,
    description: `Una descripción para tu sitio super rápido, usando múltiples temas!`,
    author: `Tu nombre`,
    social: [
      {
        name: `Twitter`,
        url: `https://twitter.com/gatsbyjs`,
      },
      {
        name: `GitHub`,
        url: `https://github.com/gatsbyjs`,
      },
    ],
  },
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        basePath: `/blog`,
      },
    },
    {
      resolve: `gatsby-theme-notes`,
      options: {
        basePath: `/notes`,
      },
    },
  ],
}
```

3. Ejecuta el sitio:

```shell
gatsby develop
```

4. Comprueba `localhost:8000` para ver lo que hay alli.

## Agregar contenido

Entre bastidores, los dos temas crearon carpetas de contenido en el directorio raíz del sitio. En este paso, agregaras algo de contenido a estas carpetas.

### Agregar un post

Crea un nuevo archivo en `/content/posts`, como este:

```mdx:title=content/posts/hello-posts.md
---
title: Mi primer post
date: 2020-02-15
---

Múltiples temas son geniales!
```

### Agregar una nota

Crea un nuevo archivo en `/content/notes`, como este:

```mdx:title=content/note/hello-notes.md
---
title: Mi primera nota
date: 2020-02-20
---

Múltiples temas son geniales!
```

Reinicia tu servidor de desarrollo con `gatsby develop`. Ahora si visitas `http://localhost:8000/blog/hello-posts/` y `http://localhost:8000/notes/hello-notes` deberías poder ver tu nuevo contenido.

## Agregar una imagen de avatar

Agrega una imagen de avatar al directorio de `content/assets/`, este es usado por `gatsby-theme-blog` para el componente de biografía. El nombre del archivo puede ser `avatar.png` o `avatar.jpg`.

## Mostrar los posts en la pagina principal

1. Elimina el archivo `src/pages/index.js` existente.

2. Cambia las opciones del tema para el blog en `gatsby-config.js`:

```javascript:title=gatsby-config.js
{
      resolve: `gatsby-theme-blog`,
      options: {
        // basePath es por defecto `/` asi que este tambien se puede incluir sin opciones, solamente con `gatsby-theme-blog`,
        basePath: `/`,
      },
    },
```

3. Reinicia tu servidor de desarrollo con `gatsby develop` para probar tu nueva página principal.

## Componentes "Shadow"

Usa [shadowing de tema](/docs/themes/shadowing/) para personalizar componentes que el tema proporciona para ti.

### Shadow `bio-content.js`

El primer componente a actualizar es `bio-content.js` que proporciona el contenido usado en el componente de `bio` en `gatsby-theme-blog`.

> 💡 No olvides detener y reiniciar tu servidor de desarrollo cuando agregues componentes "shadow" por primera vez.

Para poder hacer "shadow" en el archivo, debes ponerlo en la misma ubicación donde existe el tema. En este caso, eso significa en `src/gatsby-theme-blog/components/bio-content.js`. Así que crearas una estructura de archivos que se ve algo como esto:

```text
└── src
    ├── gatsby-theme-blog
    │   ├── components
    │   │   ├── bio-content.js // highlight-line
```

Siéntete libre de cambiar el texto de tú biografía como quieras, pero el componente se vera algo como esto:

```jsx:title=src/gatsby-theme-blog/components/bio-content.js
import React, { Fragment } from "react"
import { Styled } from "theme-ui"

export default () => (
  <Fragment>
    Palabras de <Styled.a href="http://example.com/">Tu Nombre</Styled.a>.
    <br />
    Cambia esto. Tu increíble biografía, sobre que tan genial eres!
  </Fragment>
)
```

### Shadow Theme-UI

Ambos `gatsby-theme-blog` y `gatsby-theme-notes` usan fichas de diseño de [Theme-UI](/docs/theme-ui/) para gestionar sus estilos: colores, tamaños de fuente, espaciado, etc. Puedes usar `component shadowing` para ganar control sobre estas fichas de diseño en el sitio final.

Así como con tu biografía, necesitas coincidir con la estructura de archivos del tema. En este caso, es `src/gatsby-plugin-theme-ui/index.js` y la estructura resultante se vera algo como esto:

```text
└── src
    ├── gatsby-plugin-theme-ui
    │   ├── index.js //highlight-line
```

Siéntete libre de usar cualquier color que quieras, pero aquí hay un ejemplo de como puedes hacerlo.

```javascript:title=src/gatsby-plugin-theme-ui/index.js
import merge from "deepmerge"
import defaultTheme from "gatsby-theme-blog/src/gatsby-plugin-theme-ui/index"

export default merge(defaultTheme, {
  colors: {
    background: "ghostwhite",
    text: "black",
    primary: "mediumvioletred",
    modes: {
      dark: {
        background: "indigo",
        text: "ghostwhite",
        primary: "gold",
      },
    },
  },
})
```

> Ten en cuenta que este ejemplo usa `deepmerge`. Este permite que uses la configuración de Theme-UI para cualquier parámetro que no sobreescribas en este archivo.

## Agregar otro tema

Los temas pueden ser grandes, como `gatsby-theme-blog`, pero tambien pueden ser un pequeno y discreto conjunto de componentes o funciones. Un gran ejemplo de esto es [gatsby-mdx-embed](https://gatsby-mdx-embed.netlify.com/) que agrega la habilidad de embedir contenido de redes sociales directamente en tus archivos MDX.

1. Instala el tema:

```shell
npm install @pauliescanlon/gatsby-mdx-embed
```

2. Actualiza el archivo `gatsby-config.js` y agrega `gatsby-mdx-embed` como un plugin:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    // ...siteMetadata no es cambiado.
  },
  plugins: [
    `@pauliescanlon/gatsby-mdx-embed`, // highlight-line
    {
      resolve: `gatsby-theme-blog`,
      options: {
        basePath: `/`,
      },
    },
    {
      resolve: `gatsby-theme-notes`,
      options: {
        basePath: `/notes`,
      },
    },
  ],
}
```

3. Prueba agregando un videos de Youtube a uno de tus posts:

```mdx:title=content/posts/video-post.md
---
title: Jason and Jackson Talk Themes
date: 2020-02-21
---

Aquí hay un video sobre composición y estilado de temas con J&J!

<YouTube youTubeId="6Z4p-qjnKCQ" />
```

## Agregar un menú de navegación

Usa `component shadowing` para agregar un menú de navegación. Puedes leer más acerca de como [crear menús de navegación dinamicos](/docs/creating-dynamic-navigation/) en la documentación.

1. Agrega un arreglo `menuLinks` al archivo `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `El titulo de tu sitio`,
    description: `Una descripción para tu sitio super rápido, usando múltiples temas!`,
    author: `Tu nombre`,
    // highlight-start
    menuLinks: [
      {
        name: `Blog`,
        url: `/`,
      },
      {
        name: `Notes`,
        url: `/notes`,
      },
    ],
    // highlight-end
    social: [
      // ...el arreglo social no es cambiado.
    ],
  },
  plugins: [
    // ...el arreglo de plugins no es cambiado.
  ],
}
```

2. Crea un componente de navegación:

```jsx:title=src/components/navigation.js
import React from "react"
import { Link, useStaticQuery, graphql } from "gatsby"
import { Styled, css } from "theme-ui"

export default () => {
  const data = useStaticQuery(
    graphql`
      query SiteMetaData {
        site {
          siteMetadata {
            menuLinks {
              name
              url
            }
          }
        }
      }
    `
  )
  const navLinks = data.site.siteMetadata.menuLinks
  return (
    <nav
      css={css({
        py: 2, // Forma corta de "paddingTop" y "paddingBottom"
      })}
    >
      <ul
        css={css({
          display: `flex`,
          listStyle: `none`,
          margin: 0,
          padding: 0,
        })}
      >
        {navLinks.map(link => (
          <li
            css={css({
              marginRight: 2,
              ":last-of-type": {
                marginRight: 0,
              },
            })}
          >
            <Styled.a
              css={css({
                fontFamily: `heading`,
                fontWeight: `bold`,
                textDecoration: `none`,
                ":hover": {
                  textDecoration: `underline`,
                },
              })}
              as={Link}
              to={link.url}
            >
              {link.name}
            </Styled.a>
          </li>
        ))}
      </ul>
    </nav>
  )
}
```

3. Cuando este listo, el siguiente paso es hacer "shadow" de `header.js` desde `gatsby-theme-blog`. Puedes copiar y pegar codigo del componente original como punto de inicio para tu nuevo componente hecho con "shadow".

Tu estructura de archivos deberia verse algo como esto:

`src/gatsby-theme-blog/components/header.js`

```text
└── src
    ├── gatsby-theme-blog
    │   ├── components
    │   │   ├── header.js // highlight-line
```

4. Importa el menú de navegación y agregalo al header:

> 💡 Este ejemplo de código está editado por longitud, el [componente completo puede ser visto en Github.](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-multiple-themes/src/gatsby-theme-blog/components/header.js)

```jsx:title=src/gatsby-theme-blog/components/header.js
import React from "react"
import { css } from "theme-ui"
import Navigation from "../../components/navigation" // highlight-line

export default () => {
  return (
    <header>
      <div
        css={css({
          maxWidth: `container`,
          mx: `auto`,
          px: 3,
          pt: 4,
        })}
      >
        <Navigation /> // highlight-line
      </div>
    </header>
  )
}
```

5. Ejecuta `gatsby develop` y prueba el nuevo componente de navegación.

## Resumiendo

Este tutorial te ha presentado la idea de componer múltiples temas juntos en un solo sitio de Gatsby. Los temas de Gatsby son una reinvención innovativa de la plantilla de sitio web tradicional y entender su potencial te da un nuevo conjunto de herramientas como desarrollador. Para seguir profundizando sobre esto, mira la [documentación de temas de Gatsby](/docs/themes/) y algunos de los otros recursos listados abajo.

## Que sigue?

- [Construyendo un tema](/tutorial/building-a-theme/)

## Otros recursos

- [Repositorio de ejemplo para usar múltiples temas](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-multiple-themes)
- [Guía de referencia para temas de Gatsby](/docs/themes/)
- [Curso de Egghead.io: Creando temas de Gatsby (gratis)](https://egghead.io/courses/gatsby-theme-authoring)
- [IBM y temas de Gatsby: Impulsando el impacto a través del diseño](https://www.youtube.com/watch?v=I2nh2juOKxM)
- [Configurando espacios de trabajo de yarn para desarrollo de temas de Gatsby](/blog/2019-05-22-setting-up-yarn-workspaces-for-theme-development/#reach-skip-nav)
- [Que es component shadowing?](/blog/2019-04-29-component-shadowing/)
- [Personalizando estilos en temas de gatsby con Theme-UI](/blog/2019-07-03-customizing-styles-in-gatsby-themes-with-theme-ui/)
- [Componiendo y estilando temas de Gatsby (con Brent Jackson) - Aprende con Jason](https://www.youtube.com/watch?v=6Z4p-qjnKCQ)
- [Construye un sitio personal usando temas de Gatsby (con Will Johnson) - Aprende con Jason](https://www.youtube.com/watch?v=vf2Dy_xKUno)
