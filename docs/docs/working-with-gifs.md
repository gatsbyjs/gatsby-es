---
title: Trabajando con GIFs
---

Si estás construyendo un blog con Gatsby, está la posibilidad que querrás incluir algunos GIFs animados: quién no querría incluir un GIF de una nutria bailarina o un gato?

## Incluyendo GIFs en componentes

En los componentes y páginas de Gatsby, querrás importar GIFs animados en vez de usar Gatsby Image porque de este modo optimiza los datos de la imagen para el elemento responsivo de la misma.

Aquí hay un ejemplo:

```jsx:title=pages/about.js
import React from 'react'

import Layout from '../components/layout'
import otterGIF from '../gifs/otter.gif'

const AboutPage = () => (
    return (
        <Layout>
            <img src={otterGIF} alt="Otter dancing with a fish" />
        </Layout>
    )
)

export default AboutPage;
```

## Incluyendo GIFs en el Markdown

En las páginas y entrada en Markdown, incluir un GIF animado se hace del mismo modo que una imagen estática:

```markdown
![nutria bailando con un pez](./images/dancing-otter.gif)
```

![nutria bailando con un pez](./images/dancing-otter.gif)

Los GIFs animados pueden ser bastante largos en tamaño, de todos modos, así que se cuidadoso de no hacerle sabotaje al rendimiento de tu sitio web con archivos extremadamente grandes. Podrías reducir el tamaño de los archivos [optimizando los fotogramas](https://skylilies.livejournal.com/244378.html) o convirtiéndolos a video.

## Asuntos relacionados con accesibilidad en los GIFs animados

Ten cuidado que los GIFs que "flashean" (cambian abruptamente de colores o marcos), o que se auto-reproducen pueden causar problemas para usuarios que son sensibles al movimiento. Los GIFs no deberían autoreproducirse siempre que sea posible por motivos de seguridad. Una técnica sería la de agregar controles, usando un paquete como [react-gif-player](https://www.npmjs.com/package/react-gif-player) como [un paquete sólo para el cliente](/docs/using-client-side-only-packages/).

Para más información sobre movimiento accesible:

- https://source.opennews.org/articles/motion-sick/
- https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html
