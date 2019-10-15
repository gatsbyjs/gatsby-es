---
title: Usando un tema
---

En este tutorial aprenderás cómo usar temas en Gatsby de forma práctica, mediante la creación de un nuevo sitio usando el tema oficial para blogs de Gatsby.

## Crear un nuevo sitio web usando el starter del tema para blogs

Crear un sitio usando un starter de un tema funciona de la misma forma que usar un starter normal:

```shell
gatsby new my-blog https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

## Ejecuta el sitio web

Crear un sitio nuevo a partir del starter instala todas las dependencias del tema para blogs por ti. Ahora, ejecutemos el sitio y veamos qué tenemos:

```shell
cd my-blog
gatsby develop
```

![Pantalla por defecto cuando se inicia un proyecto utilizando el starter del tema para blogs de gatsby](./images/starter-blog-theme-default.png)

## Sustituye tu avatar

El starter del tema para blogs viene con una imagen gris sólida para el avatar. Añade tu propio avatar seleccionando la imagen que quieras, y sobreescribe el fichero que se encuentra en `/content/assets/avatar.png`.

## Actualizas los metadatos de tu sitio web
Personaliza la información en tu propio sitio mediante el remplazo de los valores de los atributos de `siteMetadata` en el fichero `gatsby-config.js`.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-theme-blog",
      options: {},
    },
  ],
  // Personaliza la información en tu propio sitio:
  {/* highlight-start */}
  siteMetadata: {
    title: "My Blog",
    author: "Amberley Romo",
    description: "A collection of my thoughts and writings.",
    siteUrl: "https://amberley.blog/",
    social: [
      {
        name: "twitter",
        url: "https://twitter.com/amber1ey",
      },
      {
        name: "github",
        url: "https://github.com/amberleyromo",
      },
    ],
  },
  {/* highlight-end */}
}
```

## Remplaza el contenido de la biografía

Cuando se usan temas de Gatsby, puedes tomar ventaja de algo llamado component shadowing.

El paquete del tema para blogs de Gatsby tiene un componente que contiene la biografía del autor del sitio web. La ruta a este componente (en el paquete del tema para blogs, no en tu propio sitio web) es `gatsby-theme-blog/src/components/bio-content.js`.

Si miras al árbol de directorios de tu sitio web, verás que es parecido al siguiente:

```
my-blog
├── content
│   ├── assets
│   │   └── avatar.png
│   └── posts
│       ├── hello-world.mdx
│       └── my-second-post.mdx
├── src
│   └── gatsby-theme-blog
│       ├── components
│       │   └── bio-content.js
│       └── gatsby-plugin-theme-ui
│           └── colors.js
├── gatsby-config.js
└── package.json
```

En el directorio `src` del sitio web se encuentra el directorio `gatsby-theme-blog`. Cualquier fichero situado en esta carpeta que se corresponda con un fichero en el tema para blogs sobreescribirá el tema.

> 💡 El nombre del directorio (por ejemplo `gatsby-theme-blog`) debe reflejar exactamente el nombre del paquete del tema publicado, que en este caso es [`gatsby-theme-blog`](https://www.npmjs.com/package/gatsby-theme-blog).

Abre el fichero `bio-content.js` y realiza algunas modificaciones de su contenido:

```jsx:title=bio-content.js
export default () => (
  {/* highlight-start */}
  <Fragment>
    This is my updated bio.
    <br />
    It's shadowing the content from the theme.
  </Fragment>
  {/* highlight-end */}
)
```

Llegados a este punto, deberías tener un avatar actualizado, los detalles de tu sitio web actualizados, y la biografía actualizada:

![Captura de pantalla del proyecto con las ediciones indicadas en el tutorial](./images/starter-blog-theme-edited.png)

## Añadir tu propio contenido al blog

Ahora puedes añadir tu primer post al blog y eliminar el contenido de demostración del starter.

### Crear un nuevo post

Crea un nuevo fichero en `my-blog/content/posts`. Nómbralo como quieras (con extensión `.md` o `.mdx`), ¡y añade algo de contenido! Aquí tienes un ejemplo:

```mdx:title=my-blog/content/posts/my-first-post.mdx
---
title: My first post
date: 2019-07-03
---

This will be my very first post on this blog!
```

### Eliminar los posts de demostración

Elimina los dos posts de demostración situados en el directorio `/content/posts`:

- `my-blog/content/posts/hello-world.mdx`
- `my-blog/content/posts/my-second-post.mdx`

Reinicia el servidor de desarrollo y verás el contenido de tu blog actualizado:

![Captura de pantalla del proyecto con posts actualizados](./images/starter-blog-theme-updated-content.png)

## Cambiar el color del tema

El tema para blog viene por defecto con el color púrpura de Gatsby, pero puedes sobreescribirlo y personalizarlo como más te guste. En este tutorial vamos a cambiar algunos colores.

Abre el fichero `/src/gatsby-theme-blog/gatsby-plugin-theme-ui/colors.js`, y descomenta el código en el mismo.

```javascript:title=colors.js
{/* highlight-start */}
const blue60 = "#007acc"
const blue30 = "#66E0FF"
const blueGray = "#282c35"
{/* highlight-end */}

export default merge({}, defaultThemeColors, {
  {/* highlight-start */}
    text: blueGray,
    primary: blue60,
    heading: blueGray,
    modes: {
      dark: {
        background: blueGray,
        primary: blue30,
        highlight: blue60,
      },
    },
   {/* highlight-end */}
})
```

Ahora, en lugar de un tema púrpura tenemos un tema azul.

![Captura de pantalla del proyecto con un color de tema actualizado](./images/starter-blog-theme-updated-colors.png)

En este fichero, estamos tomando el color por defecto del tema (importado como `defaultThemeColors` aquí) y sobreescribiendo ciertos valores del mismo.

Para ver qué otros colores del tema puedes personalizar, revisa el fichero `colors.js` en el tema oficial para blogs (`gatsby-theme-blog/src/gatsby-plugin-theme-ui/colors.js`)

## Empaquetado

Esto fue una introducción paso a paso para usar un tema de Gastby a través de un ejemplo específico. Ten en cuenta que temas diferentes serán construidos de forma diferente, para permitir diversas opciones de personalización. Para más información, revisa la [documentación sobre temas de Gatsby](/docs/themes/).