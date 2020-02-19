---
title: Agregando transiciones de página con _gatsby-plugin-transition-link_
---

Esta guía cubrirá cómo usar `gatsby-plugin-transition-link` para animar transiciones entre páginas en tu sitio web Gatsby.

## Vista general

El componente `TransitionLink` provee una manera de describir la transición de una página vía _props_ en un componente Link. Funciona con muchas librerías de animación, como [react-pose](https://popmotion.io/pose/), [gsap](https://greensock.com/), [animejs](https://animejs.com/) y muchas otras.

Nota que actualmente, como el plugin está basado en _link navigation_, las transiciones no están soportadas cuando navegas con los botones del navegador.

Para otras opciones de transiciones de página, mira la [vista general de agregar animaciones de página](/docs/adding-page-transitions).

## Empezando

Primero, instala el plugin:

```shell
npm install --save gatsby-plugin-transition-link
```

Asegúrate de agregar el plugin en tu `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
    plugins: [
      `gatsby-plugin-transition-link`
    ]
];
```

Finalmente, importa el componente `TransitionLink` donde sea que quieras usarlo:

```javascript
import TransitionLink from "gatsby-plugin-transition-link"
```

## Transiciones predefinidas

Puedes usar el componente `AniLink` para agregar transiciones de página sin tener que definir tus propias transiciones. Es un envoltorio alrededor de `TransitionLink` que provee 4 transiciones predefinidas: `fade`, `swipe`, `cover`, y `paintDrip`. Puedes previsualizarlas en [este sitio demo](https://gatsby-plugin-transition-link.netlify.com/).

Para usar AniLink, necesitarás instalar la librería de animación `gsap`:

```shell
npm install --save gsap
```

Entonces, importa el componente AniLink:

```jsx
import AniLink from "gatsby-plugin-transition-link/AniLink"
```

Finalmente, asegúrate de proveer el nombre de la animación deseada como una _blank_ _prop_ a `AniLink`:

```jsx
<AniLink paintDrip to="page-4">
  Go to Page 4
</AniLink>
```

Opciones como duración de la transición, dirección y demás son configurables con _props_. Mira [la documentación de AniLink](https://transitionlink.tylerbarnes.ca/docs/anilink/) para más detalles.

## Transiciones personalizadas

Tienes dos métodos principales de crear transiciones de páginas:

1. Usa la función `trigger` definida en tu _prop_ `exit`/`entry`. Más detalles en la subsección '[Usando la función `trigger`](#using-the-trigger-function)'.
2. Usa las _props_ pasadas por `TransitionLink` para definir tus transiciones. Más detalles en la subsección '[Usando _props_ pasadas](#using-passed-props)'.

Adicionalmente, puedes especificar un número de _props_ y opciones en el componente `TransitionLink`, como `length`, `delay` y más. Para mas opciones y detalles, mira [la documentación de TransitionLink](https://transitionlink.tylerbarnes.ca/docs/transitionlink/).

#### Usando la función trigger

Puedes especificar una función `trigger` que manejará la animación. Esto es útil para las librerías de animaciones _imperativas_ como [animejs](https://animejs.com/) o [GSAP](https://greensock.com/gsap) que especifican animaciones con llamadas a funciones.

```jsx
<TransitionLink
  exit={{
    length: length,
    // highlight-next-line
    trigger: ({ exit, node }) =>
      this.someCustomDefinedAnimation({ exit, node, direction: "out" }),
  }}
  entry={{
    length: 0,
    // highlight-next-line
    trigger: ({ exit, node }) =>
      this.someCustomDefinedAnimation({ exit, node, direction: "in" }),
  }}
  {...props}
>
  {props.children}
</TransitionLink>
```

#### Usando props pasadas

La salida y entrada de páginas/plantillas involucradas en la transición recibirán _props_ indicando el estado de la transición actual, así como también la _prop_ `exit` o `enter` definida en el `TransitionLink`.

```jsx
const PageOrTemplate = ({ children, transitionStatus, entry, exit }) => {
  console.log(transitionStatus, entry, exit)
  return <div className={transitionStatus}>{children}</div>
}
```

Puedes combinar estas _props_ con una librería de animación basada-en-estado _declarativa_ como [react-pose](https://popmotion.io/pose/) o [react-spring](http://react-spring.surge.sh/) para especificar transiciones para salir y entrar a una página.

Si quieres acceder a estas _props_ en uno de tus componentes en vez de una página/plantilla, debes envolver tu componente en el componente `TransitionState`. Este componente toma una función que accederá a las mismas propiedades como antes, la cual podrás usar en tu componente.

Aquí un ejemplo usando `TransitionState` y `react-pose` para activar las transiciones _enter/exit_ para el componente `Box`.

```jsx
import { TransitionState } from "gatsby-plugin-transition-link"

const Box = posed.div({
  hidden: { opacity: 0 },
  visible: { opacity: 1 },
})

<TransitionState>
      {({ transitionStatus, exit, enter, mount }) => {
        console.log("current page's transition status is", transitionStatus)
        console.log("exit object is", exit)
        console.log("enter object is", enter)

        return (
            <Box
              className="box"
              pose={
                mount // this is true while the page is mounting or has mounted
                  ? 'visible'
                  : 'hidden'
              }
            />
        )
      }}
</TransitionState>
```

Ahora, el componente `Box` estará al pendiente del estado de la transición de la página que es hijo, y aparecerá de entrada/salida en consecuencia.

## Excluyendo elementos de las transiciones de página

Quizá quieras tener elementos en la página que persistan durante la transición de la página (_ej. una cabecera del sitio_). Esto se puede conseguir envolviendo elementos con el componente `TransitionPortal`.

```javascript
import { TransitionPortal } from "gatsby-plugin-transition-link"
```

```javascript
module.exports = {
    plugins: [
       {
          resolve: "gatsby-plugin-transition-link",
          options: {
              layout: require.resolve(`./src/components/Layout.js`)
            }
       }
    ]
];
```

Como siempre, fíjate en [la documentación de `TransitionPortal`](https://transitionlink.tylerbarnes.ca/docs/transitionportal/) para más información acerca de `TransitionPortal`.

## Siguientes lecturas

- [Documentación oficial](https://transitionlink.tylerbarnes.ca/docs/)
- [Código fuente del plugin](https://github.com/TylerBarnes/gatsby-plugin-transition-link)
- [Sitio demo](https://gatsby-plugin-transition-link.netlify.com/)
- [Entrada de blog: 'Transiciones de página con Per-Link Gatsby y TransitionLink'](/blog/2018-12-04-per-link-gatsby-page-transitions-with-transitionlink/)
- [Usando transition-link con react-spring](https://github.com/TylerBarnes/gatsby-plugin-transition-link/issues/34)
