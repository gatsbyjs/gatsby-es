---
title: Introduction to Styling in Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

<!-- Idea: Create a glossary to refer to. A lot of these terms get jumbled -->

<!--
  - Global styles
  - Component css
  - CSS-in-JS
  - CSS Modules

-->

¡Bienvenido a la parte dos del tutorial de Gatsby!

## ¿Qué abarca este tutorial?

En esta parte, explorarás opciones para estilizar páginas web de Gatsby y a la vez interiorizarte en el uso de componentes React para crear sitios web.

## Usando estilos globales

Cada sitio web tiene algún tipo de estilo global. Esto incluye cosas como la tipografía y los colores de fondo. Estos estilos definen la vista general del sitio, así como el color y las texturas de una pared definen la vista general de una habitación.

### Creando estilos globales con archivos CSS básicos

Una de las maneras más directas de agregar estilos globales a un sitio web es usando una hoja de estilos global `.css`

#### ✋ Crea un nuevo sitio web con Gatsby

Sería mejor (especialmente si eres nuevo con la línea de comandos) si cerraras el terminal que usaste para la [parte uno](/tutorial/part-one/) e inicias una nueva sesión en otra terminal para la parte dos.

<<<<<<< HEAD
Abre una nueva terminal, crea un nuevo sitio web "hola mundo" con Gatsby e inicia el servidor de desarrollo:
=======
Open a new terminal window, create a new "hello world" Gatsby site in a directory called `tutorial-part-two`, and then move to this new directory:
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

```shell
gatsby new tutorial-parte-dos https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-parte-dos
```

Ahora tienes un nuevo sitio web Gatsby (basado en el inicializador Gatsby "hola mundo") con la siguiente estructura:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
```

<<<<<<< HEAD
#### ✋ Agrega estilos a un archivo css
=======
#### ✋ Add styles to a CSS file
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

1. Crea un archivo `.css` en tu proyecto nuevo:

```shell
cd src
mkdir styles
cd styles
touch global.css
```

> Nota: puedes crear estos directorios y archivos usando tu editor de código, si así lo prefieres.

Ahora deberías tener una estructura como esta:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
```

2. Define algunos estilos en el archivo `global.css`:

```css:title=src/styles/global.css
html {
  background-color: lavenderblush;
}
```

<<<<<<< HEAD
> Nota: el lugar donde quede ubicado el archivo css de ejemplo en `/src/styles/` es irrelevante.
=======
> Note: The placement of the example CSS file in a `/src/styles/` folder is arbitrary.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### ✋ Incluye la hoja de estilos en `gatsby-browser.js`

1. Crea el `gatsby-browser.js`

```shell
cd ../..
touch gatsby-browser.js
```

La estructura de tu proyecto ahora debería verse así:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

> 💡 ¿Qué es `gatsby-browser.js`? No te preocupes demasiado de eso por ahora, ten en cuenta que `gatsby-browser.js` es uno de los pocos archivos especiales que Gatsby busca y utiliza (si existen). Aquí, el nombre de el archivo **es** importante. Si quieres saber más, revisa [la documentación](/docs/browser-apis/).

2. Importa tu hoja de estilo recientemente creada en `gatsby-browser.js`:

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"

// or:
// require('./src/styles/global.css')
```

> Nota: Ambas sintaxis CommonJS (`require`) y ES Module (`import`) funcionan. Si no sabes cuál utilizar, nosotros usamos `import` la mayoría del tiempo.

3. Inicia el servidor de desarrollo:

```shell
gatsby develop
```

Si echas un vistazo a tu proyecto en el navegador, deberías ver el fondo de atrás de color lavanda:

![Hola mundo color Lavanda](global-css.png)

> Consejo: Esta parte del tutorial se ha enfocado en la manera más rápida y directa para iniciar a estilizar un sitio web Gatsby - importando directamente archivos CSS normales, usando `gatsby-browser.js`. En la mayoría de los casos, la mejor manera de agregar estilos globales es con un componente de diseño compartido. [Revisa la documentación](/docs/global-css/) para saber más acerca de esta aproximación.

## Usando CSS limitado al componente

<<<<<<< HEAD
Hasta aquí, hemos hablado acerca de la aproximación más tradicional de usar hojas de estilo css normales. Ahora, hablaremos acerca de varios métodos de estructurar CSS para realizar estilos de una manera orientada a componentes.
=======
So far, we've talked about the more traditional approach of using standard CSS stylesheets. Now, we'll talk about various methods of modularizing CSS to tackle styling in a component-oriented way.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

### Módulos CSS

Exploremos **Módulos CSS**. Citando de
[la página Módulo CSS](https://github.com/css-modules/css-modules):

> Un **Módulo CSS** es un archivo CSS en el cual todos los nombres de las clases y animaciones
> están limitados localmente por defecto.

Los Módulos CSS son muy populares porque te permiten escribir CSS normalmente, pero con mayor confianza. La herramienta genera automáticamente nombres de clases y animaciones únicas, así que no tienes que preocuparte por colisiones de nombres en selectores de estilos.

Gatsby trabaja por defecto con Módulos CSS. Esta aproximación es muy recomendada para aquellos que son nuevos en Gatsby (y en React en general).

#### ✋ Construye una nueva página web usando Módulos CSS

En esta sección, crearás un nuevo componente de página y le darás estilo a ese componente de página usando un Módulo CSS.

Primero, crea un nuevo componente `Container`.

1. Crea un nuevo directorio en `src/components` y después, en este nuevo directorio, crea un archivo llamado `container.js` y pega lo siguiente:

```jsx:title=src/components/container.js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
)
```

<<<<<<< HEAD
Notarás que importamos un archivo llamado `container.module.css` que es un módulo css. Creemos ese archivo ahora.
=======
You'll notice you imported a CSS module file named `container.module.css`. Let's create that file now.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

2. En el mismo directorio (`src/components`), crea un archivo `container.module.css` y copia/pega lo siguiente:

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

Notarás que el archivo termina con `.module.css` en vez del clásico `.css`. Es así como le indicas a Gatsby que este archivo CSS debe ser procesado como un módulo CSS en vez de un CSS plano.

3. Crea un nuevo componente de página, creando un archivo en
   `src/pages/about-css-modules.js`:

```jsx:title=src/pages/about-css-modules.js
import React from "react"

import Container from "../components/container"

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
)
```

Ahora, si visitas `http://localhost:8000/about-css-modules/`, tu página debería verse algo parecido a esto:

![Página con estilos de módulos CSS](css-modules-basic.png)

#### ✋ Dale estilo a un componente utilizando Módulos CSS

En esta sección, crearás una lista de personas con sus nombres, avatares y una biografía corta en latín. Crearás un componente `<User />` y le darás estilo a ese componente utilizando un módulo CSS.

1. Crea el archivo para el CSS en `src/pages/about-css-modules.module.css`.

2. Pega lo siguiente dentro del archivo nuevo:

```css:title=src/pages/about-css-modules.module.css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

3. Importa el nuevo archivo `src/pages/about-css-modules.module.css` en la página `about-css-modules.js` que creaste recientemente editando las primeras líneas del archivo de la siguiente manera:

```javascript:title=src/pages/about-css-modules.js
import React from "react"
// highlight-next-line
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

// highlight-next-line
console.log(styles)
```

El código `console.log(styles)` registrará en consola lo importado para que puedas apreciar el resultado de procesar el archivo `./about-css-modules.module.css`. Si abres la consola de desarrollador (usando por ejemplo las herramientas de desarrollador de Firefox o Chrome, usualmente por la tecla F12) en tu navegador, verás:

![Resultado de importar módulos CSS en consola](css-modules-console.png)

Si comparas eso contra tu archivo CSS, observarás que cada clase es ahora una llave en el objeto importado apuntando a una cadena larga, por ejemplo `avatar` apunta a `src-pages----about-css-modules-module---avatar---2lRF7`. Estos son los nombres de clase que genera Módulos CSS. Está garantizado que serán únicas en todo tu sitio web. Y debido a que tienes que importarlas para usar las clases, nunca habrá ninguna duda de donde se está usando algo de CSS.

4. Crea un componente `User`.

Crea un nuevo componente `<User />` en el mismo archivo del componente de página `about-css-modules.js`.
Modifica `about-css-modules.js` para que se vea así:

```jsx:title=src/pages/about-css-modules.js
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

console.log(styles)

// highlight-start
const User = props => (
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>{props.username}</h2>
      <p className={styles.excerpt}>{props.excerpt}</p>
    </div>
  </div>
)
// highlight-end

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
    {/* highlight-start */}
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    {/* highlight-end */}
  </Container>
)
```

> Consejo: Generalmente, si tu miras a un componente en diferentes partes de un sitio web, debería estar en su propio archivo de módulo en el directorio `components`. Pero, si es usado solo en un archivo, crealo ahí mismo.

El resultado final de la página web debería verse así:

![Página de listado de usuarios con módulos CSS](css-modules-userlist.png)

### CSS-in-JS

CSS-in-JS es un enfoque de estilizado orientado a componentes. En general, es un patrón en donde [el CSS es escrito en línea usando JavaScript](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js).

#### Usando CSS-in-JS con Gatsby

Hay muchas bibliotecas diferentes de CSS-in-JS y muchas de ellas ya tienen algún plugin de Gatsby. En este tutorial de inicio no cubrimos ningún ejemplo de CSS-in-JS, pero te animamos a que [explores](/docs/styling/) lo que el ecosistema tiene para ofrecerte. Existen mini-tutoriales para dos bibliotecas, en particular, [Emotion](/docs/emotion/) y [Styled Components](/docs/styled-components/).

#### Lecturas sugeridas de CSS-in-JS

Si estás interesado en leer más, consulta la presentación de 2014 de [Christopher "vjeux" Chedeau que provocó este movimiento](https://speakerdeck.com/vjeux/react-css-in-js) así como la publicación más reciente de [Mark Dalgleish "A Unified Styling Language"](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

### Otras opciones CSS

Gatsby ofrece compatibilidad con casi cualquier opción de estilizado (si no existe algún plugin aún para tu opción CSS favorita, [¡por favor contribuye con uno!](/contributing/how-to-contribute/))

- [Typography.js](/packages/gatsby-plugin-typography/)
- [Sass](/packages/gatsby-plugin-sass/)
- [JSS](/packages/gatsby-plugin-jss/)
- [Stylus](/packages/gatsby-plugin-stylus/)
- [PostCSS](/packages/gatsby-plugin-postcss/)

¡y más!

## ¿Qué viene después?

Ahora continúa a la [parte tres del tutorial](/tutorial/part-three/), donde aprenderás acerca de los plugins de Gatsby y componentes de diseño.
