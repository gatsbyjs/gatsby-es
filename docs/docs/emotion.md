---
title: Emotion
---

En esta guía, aprenderás como configurar un sitio con la librería CSS-in-JS [Emotion](https://emotion.sh).

Emotion es una librería de CSS-in-JS flexible y eficaz. Basándose en muchas otras librerías CSS-in-JS, te permite dar estilo a tus aplicaciones rápidamente con estilos en objetos o en strings. Tiene una composición predecible para evitar problemas de especificidad con el CSS. Con _source maps_ y etiquetas, Emotion tiene una excelente _developer experience_ y un gran rendimiento gracias al intensivo almacenamiento en caché en producción.

El [renderizado en servidor](https://emotion.sh/docs/ssr) funciona _out of the box_ en Emotion. Puedes usar métodos de React como `renderToString` o `renderToNodeStream` directamente sin configuración adicional. La característica `extractCritical` elimina las reglas sin usar que hayan sido creadas con Emotion lo que ayuda a cargar las páginas más rápido.

Primero, abre una nueva ventana de terminal y ejecuta el siguiente comando para crear un nuevo sitio:

```shell
gatsby new emotion-tutorial https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Después, instala las dependencias necesarias para Emotion y Gatsby.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

Y entonces añade el siguiente plugin al `gatsby-config.js` de tu sitio:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
};
```

Después ejecuta `npm start` en tu terminal para iniciar el servidor de desarrollo de Gatsby.

Ahora vamos a crear una página de ejemplo con Emotion en `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import styled from "@emotion/styled"
import { css } from "@emotion/core"

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const UserWrapper = styled.div`
  display: flex;
  align-items: center;
  margin-top: 0;
  margin-right: auto;
  margin-bottom: 12px;
  margin-left: auto;
  &:last-child {
    margin-bottom: 0;
  }
`

const Avatar = styled.img`
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Description = styled.div`
  flex: 1;
  margin-left: 18px;
  padding: 12px;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const Excerpt = styled.p`
  margin: 0;
`
// Usando la prop css proporciona una API flexible y concisa para dar estilo a tus componentes //
const underline = css`
  text-decoration: underline;
`

const User = props => (
  <UserWrapper>
    <Avatar src={props.avatar} alt="" />
    <Description>
      <Username>{props.username}</Username>
      <Excerpt>{props.excerpt}</Excerpt>
    </Description>
  </UserWrapper>
)

export default () => (
  <Container>
    <h1 css={underline}>Sobre Emotion</h1>
    <p>Emotion es súper genial</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="Soy Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="Soy Bob smith, esa clase de tío verticalmente alineado. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
  </Container>
)
```

## Añadiendo estilos globales en Gatsby con Emotion

Para empezar, crea un nuevo sitio Gastby con el [_hello world starter_](https://github.com/gatsbyjs/gatsby-starter-hello-world) e instala [`gatsby-plugin-emotion`](/packages/gatsby-plugin-emotion/) y sus dependencias:

```shell
gatsby new global-styles https://github.com/gatsbyjs/gatsby-starter-hello-world
cd global-styles
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

Crea el fichero `gatsby-config.js` y añade el plugin de Emotion:

```js:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

Después, añade un componente _layout_ en `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react";
import { Global, css } from "@emotion/core";
import styled from "@emotion/styled";

const Wrapper = styled("div")`
  border: 2px solid green;
  padding: 10px;
`

export default ({ children }) => (
  <Wrapper>
    <Global
      styles={css`
        div {
          background: red;
          color: white;
        }
      `}
    />
    {children}
  </Wrapper>
)
```

Entonces, actualiza `src/pages/index.js` usando el _layout_:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>¡Hola mundo!</Layout>
```

Ejecuta `npm run build`, y ya puedes ver en `public/index.html` que los estilos globales han sido añadidos _inline_.
