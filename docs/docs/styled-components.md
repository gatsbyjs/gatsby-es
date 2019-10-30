---
title: Styled Components
---

En esta guía, aprenderás cómo configurar un sitio con la librería CSS-in-JS, [Styled Components](https://www.styled-components.com/).

Styled Components nos permite usar nuestra sintaxis real de CSS en nuestros componentes. Styled Components es una variante de "CSS-in-JS" que resuelve muchos de los problemas del CSS tradicional.

Uno de los problemas más importantes que resuelve es la colisión de selectores. Con el CSS tradicional, tienes que ser cuidadoso de no sobrescribir los selectores CSS usados en cualquier lugar de tu sitio, porque todos los selectores viven en el mismo espacio de nombres global. Esta desafortunada restricción puede acabar con una elaborada (y a veces confusa) forma de nombrar los selectores.

Con CSS-in-JS, evitas todo eso ya que los selectores CSS están aislados automáticamente en su componente. Los estilos están estrechamente ligados a sus componentes. Esto hace mucho más fácil saber cómo editar el CSS de un componente ya que no habrá nunca ninguna confusión de cómo y dónde el CSS está siendo usado.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components"
  lessonTitle="Da estilos a sitios hechos con Gatsby con styled-components"
/>

Primero, abre una nueva ventana de terminal y ejecuta el siguiente comando para crear un nuevo sitio:

```shell
gatsby new styled-components-tutorial https://github.com/gatsbyjs/gatsby-starter-hello-world
cd styled-components-tutorial
```

Segundo, instala las dependencias necesarias para `styled-components`, incluyendo el plugin de Gatsby.

```shell
npm install --save gatsby-plugin-styled-components styled-components babel-plugin-styled-components
```

Y después añádelo al `gatsby-config.js` de tu sitio:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

Después ejecuta `npm start` en tu terminal para iniciar el servidor de desarrollo de Gatsby.

Ahora vamos a crear una página de ejemplo con Styled Components en `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"
import styled from "styled-components"

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
  margin: 0 auto 12px auto;
  &:last-child {
    margin-bottom: 0;
  }
`

const Avatar = styled.img`
  flex: 0 0 96px;
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
    <h1>Sobre Styled Components</h1>
    <p>Styled Components es genial</p>
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

### Habilitando _user stylesheets_ con nombre de clase estable

Añadiendo un CSS `className` persistente a tus _styled components_ puedes hacer más fácil para los usuarios finales de tu sitio web tomar ventaja de las [_user stylesheets_](https://www.viget.com/articles/inline-styles-user-style-sheets-and-accessibility/) para accesibilidad.

Aquí está un ejemplo donde el nombre de clase `container` es añadido al DOM junto con los nombres de clase creados dinámicamente del _Styled Components_:

```jsx:title=src/components/container.js
import React from "react"
import styled from "styled-components"

const Section = styled.section`
  margin: 3rem auto;
  max-width: 600px;
`

export default ({ children }) => (
  <Section className={`container`}>{children}</Section>
)
```

Un usuario final de tu sitio podría entonces [escribir sus propios estilos CSS](https://mediatemple.net/blog/tips/bend-websites-css-will-stylish-stylebot/) de los elementos HTML correspondientes usando el nombre de clase `.container`. Si tu CSS-in-JS cambia, no afectará a la hoja de estilo de tu usuario final.

```css:title=user-stylesheet.css
.container {
  margin: 5rem auto;
  font-size: 1.3rem;
}
```
