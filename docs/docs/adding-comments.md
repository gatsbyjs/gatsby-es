---
title: Agregando comentarios
---

Si tienes un blog corriendo en Gatsby y has empezado a agregar contenido a el, lo siguiente en lo que deberías pensar es en cómo incrementar el “engagement” entre tus visitantes. Una buena forma de hacerlo es permitir que tus usuarios puedan realizar preguntas y expresen sus puntos de vista sobre lo que has escrito. Esto hará ver tu blog mucho más dinámico para cualquiera que lo visite.

Existen muchas opciones para añadir funcionalidad de comentarios, muchos de ellos están enfocados especialmente a sitios estáticos. Aunque esta lista no es de ninguna manera exhaustiva, plantea un buen punto de inicio para ilustrar que hay disponible:

- [Disqus](https://disqus.com)
- [Commento](https://commento.io)
- [Facebook Comments](https://www.npmjs.com/package/react-facebook)
- [Staticman](https://staticman.net)
- [JustComments](https://just-comments.com) \([Plugin oficial de Gatsby](https://www.gatsbyjs.org/packages/gatsby-plugin-just-comments/)\)
- [TalkYard](https://www.talkyard.io)
- [Gitalk](https://gitalk.github.io)

Puedes también [crear tu propio sistema de comentarios](/blog/2019-08-27-roll-your-own-comment-system/), como Tania Rascia escribió en el blog de Gatsby.

## Usando Disqus para comentarios

En esta guía te mostraremos como implementar Disqus en tu blog, ya que tiene características atractivas.

- Es de bajo mantenimiento, es decir, [moderar tus comentarios y mantener tu audiencia](https://help.disqus.com/moderation/moderating-101) es fácil.
- Provee [soporte oficial de React](https://github.com/disqus/disqus-react).
- Ofrece un [plan gratis muy generoso](https://disqus.com/pricing).
- [Parece ser por mucho el servicio más usado](https://www.datanyze.com/market-share/comment-systems/disqus-market-share).
- Es fácil comentar: Disqus tiene una gran base de usuarios y la experiencia de integración de nuevos usuarios es rápida. Puedes registrarte con tu cuenta de Google, Facebook o Twitter y los usuarios pueden compartir fácilmente los comentarios que escriben a través de esos canales.
- La interfaz de Disqus tiene una inconfundible pero discreta apariencia que muchos usuarios reconocerán y confiarán en ella.
- Todos los componentes de Disqus son "lazy-loaded", es decir, no impactarán en el tiempo de carga de tus entradas del blog.

Sin embargo, ten en mente que usar Disqus también involucra un sacrificio. Tu sitio ya no es completamente estático, pues depende de una plataforma externa para enviar sus comentarios a través de `iframe`s integrados al momento en que el sitio cargue. Además, debes considerar las implicaciones de privacidad por permitir que un tercero guarde los comentarios de tus visitantes y potencialmente puedan seguir sus historiales de navegación. Puedes consultar el [aviso de privacidad de Disqus](https://help.disqus.com/terms-and-policies/disqus-privacy-policy), [preguntas frecuentes de privacidad](https://help.disqus.com/terms-and-policies/privacy-faq) (especialmente la última pregunta acerca del cumplimiento de GDPR) e informar a tus usuarios [como editar su configuración de difusión de datos](https://help.disqus.com/terms-and-policies/how-to-edit-your-data-sharing-settings).

Si estos problemas son más grandes que los beneficios de usar Disqus, puedes optar por alguna de las siguientes opciones. Aceptamos pull requests para expandir esta guía con instrucciones de configuración para otros servicios.

## Implementando Disqus

![Logo de Disqus](images/disqus-logo.svg)

Pasos para agregar comentarios de Disqus a tu propio blog:

1. [Registrarse a Disqus](https://disqus.com/profile/signup). Durante el proceso tendrás que escoger un nombre corto para tu sitio. De esta forma Disqus identificará comentarios viniendo de tu sitio. Guarda el nombre para después.
2. Instalar el paquete Disqus React

```shell
npm install disqus-react
```

3. Agregar el nombre que utilizaste en el paso 1 como, por ejemplo, `GATSBY_DISQUS_NAME` a tus archivos `.env` y `.env.example` para que las personas que hagan fork de tu repositorio sepan que ellos necesitan ingresar este valor para hacer funcionar los comentarios (Necesitas el prefix de la variable de entorno con `GATSBY_` para que pueda estar [disponible en el código cliente](https://www.gatsbyjs.org/docs/environment-variables/#client-side-javascript).)

```title=.env.example
# habilita comentarios de Disqus para posts en un blog
GATSBY_DISQUS_NAME=insertValue
```

```title=.env
GATSBY_DISQUS_NAME=yourSiteShortname
```

4. En la plantilla de tu entrada de blog (usualmente `src/templates/post.js`) importa el componente `DiscussionEmbed`.

```js:title=src/templates/post.js
import React from "react"
import { graphql } from "gatsby"
// highlight-next-line
import { DiscussionEmbed } from "disqus-react"
```

Luego define tu objeto de configuración de Disqus

```js
const disqusConfig = {
  shortname: process.env.GATSBY_DISQUS_NAME,
  config: { identifier: slug, title },
}
```

Donde `identifier` debe ser un string o número que identifique exclusivamente a esa entrada de blog. Puede ser el slug del post, título o un ID. Finalmente, agrega `DiscussionEmbed` al JSX de la plantilla de tu entrada de blog.

```js:title=src/templates/post.js
return (
  <Global>
    <PageBody>
      {/* highlight-next-line */}
      <DiscussionEmbed {...disqusConfig} />
    </PageBody>
  </Global>
)
```

Y eso es todo. Ahora debes poder ver el formulario de comentarios de Disqus debajo del post de tu blog [de esta forma](https://janosh.io/blog/disqus-comments#disqus_thread). ¡Feliz blogging!

[![Comentarios de Disqus](images/disqus-comments.png)](https://janosh.io/blog/disqus-comments#disqus_thread)
