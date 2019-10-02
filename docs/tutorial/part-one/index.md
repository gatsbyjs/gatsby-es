---
title: Conoce los bloques de construcción de Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

En la [sección anterior](/tutorial/part-zero/), preparaste tu ambiente local de desarrollo instalando el software necesario y creando tu primer sitio con Gatsby utilizando el [**starter "hello world"**](https://github.com/gatsbyjs/gatsby-starter-hello-world). Ahora, mira en profundidad el código generado por el starter.

## Utilizando starters de Gatsby

En la [parte cero del tutorial](/tutorial/part-zero/), creaste un nuevo sitio basado en el starter "hello world", utilizando el comando:

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Cuando se crea un nuevo sitio con Gatsby, puedes utilizar la siguiente estructura de comando para crear un sitio nuevo basado en cualquier starter de Gatsby existente:

```shell
gatsby new [NOMBRE_DEL_DIRECTORIO] [URL_DEL_REPOSITORIO_DEL_STARTER]
```

Si omites el URL del final, Gatsby automaticamente generará un sitio para ti basado en el [starter por defecto](https://github.com/gatsbyjs/gatsby-starter-default). Para esta sección del tutorial, continua con el sitio "Hello World" que ya creaste en la parte cero del tutorial.

### ✋ Abriendo el código

En tu editor de código, abre el código generado por tu sitio "Hello World" y dale un vistazo a los diferentes directorios y archivos que se encuentran en el directorio ‘hello-world’. Debería verse como algo así:

![Hello World project in VS Code](01-hello-world-vscode.png)

_Note: De nuevo, el editor mostrado aquí es Visual Studio Code. Si estás utilizando un editor diferente, se vera un poco diferente._

Echemos un vistazo al código que alimenta a la página principal.

> 💡 Si detuviste tu servidor de desarrollo despues de correr `gatsby develop` en la sección anterior, inicialo de nuevo ahora - es hora de hacer algunos cambios al sitio hello-world!

## Familiarizandote con páginas de Gatsby

Abre el directorio `src` en tu editor de código. Adentro hay un solo directorio: `/pages`.

Abre el archivo en `src/pages/index.js`. El código en este archivo crea un componente que contiene un solo div y algo de texto - apropiadamente, "Hello world!"

### ✋ Haz cambios a la página principal "Hello World"

1.  Cambia el texto "Hello World" a "Hola Gatsby!" y guarda el archivo. Si tus ventanas estan una al lado de la otra, puedes ver que los cambios a tu código y contenido son reflejados casi de inmediato en el navegador despues de guardar el archivo.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./02-demo-hot-reloading.mp4"></source>
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

> 💡 Gatsby utilizado **recarga en caliente** para incrementar la velocidad del desarrollo. Esensialmente, cuando estas utilizando un sservidor de desarrollo de Gatsby, los archivos del sitio de Gatsby estan siendo "mirados" en segundo plano - cuando sea que guardes el archivo, tus cambios serán inmediatamente reflejados en el navegador. No necesitas recargar a mano la página o reiniciar el servidor de desarrollo - tus cambios solo aparecerán.

2.  Ahora puedes hacer que tus cambios sean un poco mas visibles. Intenta reemplazando el código en `src/pages/index.js` con el código de abajo y guarda de nuevo. Verás los cambios al texto - el color del texto sera purpura y el tamaño de la fuente sera más grande.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hola Gatsby!</div>
)
```

> 💡 We’ll be covering more about styling in Gatsby in [**part two**](/tutorial/part-two/) of the tutorial.

3.  Quita el estilo del tamaño de la fuente, cambia el texto de "Hola Gatsby!" a un encabezado de primer nivel, y agrega un parrafo debajo del encabezado.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  {/* highlight-start */}
  <div style={{ color: `purple` }}>
    <h1>Hola Gatsby!</h1>
    <p>Que mundo.</p>
  {/* highlight-end */}
  </div>
)
```

![Más cambios con recarga en caliente](03-more-hot-reloading.png)

4.  Agrega una imagen. (En este caso, una imagen al azar de Unsplash).

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple` }}>
    <h1>Hola Gatsby!</h1>
    <p>Que mundo.</p>
    {/* highlight-next-line */}
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

![Agregar imagen](04-add-image.png)

### Espera… HTML en nuestro Javascript? 

_Sí estas familizarizado con React, sientete libre de saltarte esta sección_ Sí no has trabajado con el framework de React antes, quizas te estes preguntando que hace HTML en una función de Javascript. O por qué estamos importando `react` en la primera línea pero pareciera que no se usa en ningun lado. Este híbrido de "HTML-in-JS" es en realidad una extensión de sintaxis de Javascript, para React, llamada JSX. Puedes seguir este tutorial sin experiencia previa con React, pero si eres curioso, aquí hay una pequeña introducción…

Considera el contenido original del archivo `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

En Javascript puro, se vería algo como esto:

```javascript:title=src/pages/index.js
import React from "react"

export default () => React.createElement("div", null, "Hello world!")
```

Ahora si puedes ver el uso de la importación de `'react'`! Pero espera. Estas escribiendo JSX, no HTML puro y Javascript. Como puede el navegador leer eso? La respuesta corta es: No lo hace. Los sitios de Gatsby vienen con herramientas ya configuradas para convertir tu código fuente en algo que los navegadores puedan interpretar.

## Construyendo con componentes

La página principal en la que estabas realizando cambios fue creada definiendo un componente de página. Que es exactamente un "componente"?

En general, un componente es un bloque de construcción para tu sitio; Es una pieza autónoma que describe una sección de la UI (interfaz de usuario).

Gatsby es construido con React. Cuando hablamos de utilizar y definir **componentes**, en realidad hablamos de **componentes de React** - piezas autónomas de código (usualmente escritas con JSX) que puedes recibir entradas y devolver elementos de React describiendo una sección de la interfaz de usuario.

Uno de los grandes cambios mentales que haces cuando empiezas a construir con componentes (si ya eres un desarrollador) es que ahora tu CSS, HTML y Javascript estan estrechamente acoplados y viviendo usualmente en el mismo archivo.

Parece aparentemente un cambio simple, pero esto tiene unas implicaciones profundas en como piensas para construir sitios web.

Toma el ejemplo de crear un boton personalizado. En el pasado, hubieses creado una clase CSS (quizás `.primary-button`) con unos estilos personalizados y entonces donde quisieras aplicar esos estilos, por ejemplo:

```html
<button class="primary-button">Haz click</button>
```

En el mundo de los componentes, en su lugar creas un componente `PrimaryButton` con los estilos de tu boton y lo usas en todo tu sitio como:

<!-- prettier-ignore -->
```jsx
<PrimaryButton>Haz click</PrimaryButton>
```

Los componentes se transforman en los bloques de construcción base de tu sitio. En lugar de estar limitado a los bloques de construcción que el navegador provee, por ejemplo `<button />`, puedes crear fácilmente nuevos bloques de construcción que cumplen elegantemente las necesidades de tus proyectos.

### ✋ Utilizando componentes de página

Cualquier componente de React definido en `src/pages/*.js` se convertirá automáticamente en una página. Veamos esto en acción.

Ya tienes un archivo `src/pages/index.js` que se convierte en un starter "Hello World". Creemos una página "Acerca".

1.  Crea un nuevo archivo en `src/pages/about.js`, copia el siguiente código en ese archivo nuevo, y guardalo.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div style={{ color: `teal` }}>
    <h1>Acerca de Gatsby</h1>
    <p>Wow. Muy React.</p>
  </div>
)
```

2.  Navega a http://localhost:8000/about/.

![Nueva página acerca de Gatsby](05-about-page.png)

Solo con poner un componente de React en el archivo `src/pages/about.js`, ahora tienes una página accesible en `/about`.

### ✋ Utilizando sub-componentes

Digamos que la página principal y la de "acerca" se vuelven algo grandes y estas reescribiendo un monton de cosas. Puedes utilizar sub-componentes para separar la interfaz de usuario en piezas reusables. Ambas páginas tienen encabezados `<h1>` - crea un componente al que te refiraras como `Header`.

1.  Crea un nuevo directorio en `src/components` y un archivo adentro del directorio llamado `header.js`.
2.  Agrega el código a continuación al nuevo archivo `src/components/header.js`.

```jsx:title=src/components/header.js
import React from "react"

export default () => <h1>Esto es un encabezado.</h1>
```

3.  Modifica el archivo `about.js` para que importe el componente `Header`. Reemplaza el `h1` del código con `<Header />`:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header" // highlight-line

export default () => (
  <div style={{ color: `teal` }}>
    <Header /> {/* highlight-line */}
    <p>Wow. Muy React.</p>
  </div>
)
```

![Agregando un componente de Encabezado](06-header-component.png)

En el navegador, el encabezado de "Acerca de Gatsby" ahora debería ser reemplazado con "Esto es un encabezado.". Pero, no quieres que tu página de "acerca" diga "Esto es un encabezado.", quieres que diga, "Acerca de Gatsby".

4.  Vuelve a `src/components/header.js` y agrega el siguiente cambio:

```jsx:title=src/components/header.js
import React from "react"

export default props => <h1>{props.headerText}</h1> {/* highlight-line */}
```

5.  Vuelve a `src/pages/about.js` y agrega el siguiente cambio:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="Acerca de Gatsby" /> {/* highlight-line */}
    <p>Wow. Muy React.</p>
  </div>
)
```

![Pasando datos al Encabezado](07-pass-data-header.png)

Ahora deberías ver el texto de tu encabezado "Acerca de Gatsby" de nuevo.

### Que son “props” o propiedades?

Antes definiste componentes de React como piezas reusables de codigo que describen la interfaz de usuario. Para hacer que estas piezas reusables sean dinamicas necesitas poder suministrarles diferentes datos. Haces eso con una entrada llamada "props". Las props son (valga la redundancia) propiedades suministradas a componentes de React.

En `about.js` pasaste una prop `headerText` con el valor de `"Acerca de Gatsby"` al sub-componente importado `Header`:

```jsx:title=src/pages/about.js
<Header headerText="Acerca de Gatsby" />
```

Arriba en `header.js`, el componente de encabezado espera recibir la prop `headerText` (debido a que lo escribiste para que esperara eso). Asi que puedes acceder a ella como:

```jsx:title=src/components/header.js
<h1>{props.headerText}</h1>
```

> 💡 En JSX, puedes embedir cualquier expresion Javascript envolviendola con un `{}`. Asi es como puedes acceder a la propiedad `headerText` (o "prop!") desde el objeto "props".

Si has pasado otra prop a nuestro componente `<Header />`, como por ejemplo...

```jsx:title=src/pages/about.js
<Header headerText="Acerca de Gatsby" arbitraryPhrase="es al azar" />
```

...habrias sido capaz de tambien acceder a la prop `arbitraryPhrase` mediante: `{props.arbitraryPhrase}`.

1.  Para enfatizar como esto hace a los componentes reusables, agrega un componente `<Header />` adicional a tu pagina "Acerca de Gatsby", agrega codigo a continuacion al archivo `src/pages/about.js`, y guardalo.

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="Acerca de Gatsby" />
    <Header headerText="Es bastante genial" /> {/* highlight-line */}
    <p>Wow. Muy React.</p>
  </div>
)
```

![Encabezado duplicado para mostrar reusabilidad](08-duplicate-header.png)

Y ahi lo tienes; un segundo encabezado - sin tener que reescribir ningun codigo - solamente pasando diferentes datos utilizando props.

### Utilizando componentes de layout

Los componentes de layout son para secciones de un sitio que quieres compartir en multiples paginas. Por ejemplo, los sitios de Gatsby comunmente tienen un componente de layout con un encabezado y un pie de pagina compartidos. Otras cosas en comun que agregar a los layouts incluyen las barras laterales y/o menus de navegacion.

Exploraras los componentes de layout en la [parte tres](/tutorial/part-three/).

## Enlazado entre paginas

Eventualmente querras enlazar entre paginas - Veamos como se enrutea en un sitio de Gatsby.

### ✋ Utilizando el componente `<Link />`

1.  Abre el componente de la pagina principal (`src/pages/index.js`), importa el componente `<Link />` de Gatsby, agrega un componente `<Link />` arriba del encabezado, y agregale una propiedad `to` con el valor de `"/contact/"` para el nombre de ruta.

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import Header from "../components/header"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contacto</Link> {/* highlight-line */}
    <Header headerText="Hola Gatsby!" />
    <p>Que mundo.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

Cuando haces click al nuevo enlace "Contacto" en la pagina principal, deberias ver...

![Pagina de desarrollo 404 de Gatsby](09-dev-404.png)

...la pagina de desarrollo 404 de Gatsby. Por que? Porque estas intentando enlazar a una pagina que no existe aun.

2.  Ahora tendras que crear un componente de pagina para la nueva pagina de "Contacto" en `src/pages/contact.js` y tenerla enlazada de nuevo a la pagina principal:

```jsx:title=src/pages/contact.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Link to="/">Pagina principal</Link>
    <Header headerText="Contacto" />
    <p>Envianos un mensaje!</p>
  </div>
)
```

Despues de que guardes el archivo, deberias ver la pagina de contacto y ser capaz de enlazarla a la pagina principal.

<video controls="controls" loop="true">
  <source type="video/mp4" src="./10-linking-between-pages.mp4"></source>
  <p>Sorry! You browser doesn't support this video.</p>
</video>

The Gatsby `<Link />` component is for linking between pages within your site. For external links to pages not handled by your Gatsby site, use the regular HTML `<a>` tag.

## Desplegando un sitio de Gatsby

Gatsby.js es un _generador de sitios moderno_, lo que significa que no hay servidores que configurar o complicadas bases de datos para desplegar. En su lugar, el comando `build` de Gatsby produce un directorio de HTML estatico y archivos Javascript que puedes desplegar a un servicio de alojamiento estatico.

Prueba utilizar [Surge](http://surge.sh/) para desplegar tu primer sitio web con Gatsby. Surge es uno de muchos "alojamientos de sitios estaticos" que hace posible desplegar sitios con Gatsby.

Si no lo has instalado anteriormente &amp; instala Surge, abre una nueva ventana de la terminal e instala su herramienta para linea de comandos:

```shell
npm install --global surge

# Despues, crea una cuenta (gratis) con ellos
surge
```

Luego, compila tu sitio ejecutando el siguiente comando en la terminal en la raiz de tu sitio (consejo: asegurate de estar ejecutando este comando en la raiz de tu sitio, en este caso en la carpeta "hello-world", que puedes hacer abriendo una nueva pestania en la misma ventana en la que ejecutaste `gatsby develop`):

```shell
gatsby build
```

El compilado deberia tardar entre 15 a 30 segundos. Una vez que el compilado finalice, es interesante dar un vistazo a los archivos que el comando `gatsby build` ha preparado para desplegar.

Echa un vistazo a la lista de archivos generados escribiendo el siguiente comando de terminal en la raiz de tu sitio, que te permitira ver el directorio `public`:

```shell
ls public
```

Entonces finalmente despliega tu sitio publicando los archivos generados a surge.sh.

```shell
surge public/
```

Una vez que esto termina de ejecutarse, deberias ver en tu terminal algo como esto:

![Captura de pantalla de publicar un sitio con Gatsby mediante Surge](surge-deployment.png)

Abre la direccion web que aparece listada en la linea de abajo `lowly-pain.surge.sh` para este
caso) y veraz tu nuevo sitio publicado! Excelente trabajo!

## ➡️ Que sigue?

En esta seccion has:

- Aprendido acerca de los starters de Gatsby, y como usarlos para crear nuevos proyectos
- Aprendido sobre sintaxis JSX
- Aprendido sobre componentes
- Aprendido sobre componentes de pagina de Gatsby y sub-componentes
- Aprendido sobre "props" de React y reusar componentes de React

Ahora, continua a [**agregando estilos a nuestro sitio**](/tutorial/part-two/)!
