---
title: Agregando transiciones de página con _gatsby-plugin-transition-link_
---

This guide will cover how to use `gatsby-plugin-transition-link` to animate transitions between pages on your Gatsby site.
Esta guía cubrirá como usar `gatsby-plugin-transition-link` para animar transiciones entre páginas en tu sitio web Gatsby.

## Overview
## Vista general

The `TransitionLink` component provides a way of describing a page transition via props on a Link component. It works with many animation libraries, like [react-pose](https://popmotion.io/pose/), [gsap](https://greensock.com/), [animejs](https://animejs.com/), and many others.
El componente `TransitionLink` provee una manera de describir la transición de una página via _props_ en un componente Link. Funciona con muchas librerias de animación, como [react-pose](https://popmotion.io/pose/), [gsap](https://greensock.com/), [animejs](https://animejs.com/) y muchas otras.

Note that currently, as the plugin is based on link navigation, transitions when navigating with the browser buttons are not supported.
Nota que actualmente, como el plugin esta basado en _link navigation_, las transiciones no están soportadas cuando navegas con los botones del navegador.

For other page transition options, see the [overview on adding page animations](/docs/adding-page-transitions).
Para otras opciones de transiciones de página, mira la [vista general en agregar animaciones de página](/docs/adding-page-transitions).

## Getting started
## Empezando

First, install the plugin:
Primero, instala el plugin:

```shell
npm install --save gatsby-plugin-transition-link
```

Make sure to add the plugin to your `gatsby-config.js`:
Asegurate de agregar el plugin en tu `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
    plugins: [
      `gatsby-plugin-transition-link`
    ]
];
```

Finally, import the `TransitionLink` component wherever you want to use it:
Finalmente, importa el componente `TransitionLink` donde quiera que quieras usarlo:

```javascript
import TransitionLink from "gatsby-plugin-transition-link"
```

## Predefined transitions
## Transiciones predefinidas

You can use the `AniLink` component to add page transitions without having to define your own custom transitions. It's a wrapper around `TransitionLink` that provides 4 predefined transitions: `fade`, `swipe`, `cover`, and `paintDrip`. You can preview them at [this demo site](https://gatsby-plugin-transition-link.netlify.com/).
Puedes usar el componente `AniLink` para agregar transiciones de página sin tener que definir tus propias transiciones. Es un envoltorio alrededor de `TransitionLink` que provee 4 transiciones predefinidas: `fade`, `swipe`, `cover`, y `paintDrip`. Puedes previsualizarlas en [este sitio demo](https://gatsby-plugin-transition-link.netlify.com/).

To use AniLink, you will need to install the `gsap` animation library:
Para usar AniLink, necesitaras instalar la librería de animación `gsap`:

```shell
npm install --save gsap
```

Then, import the AniLink component:
Entonces, importa el componente AniLink:

```javascript
import AniLink from "gatsby-plugin-transition-link/AniLink"
```

Finally, make sure you provide your desired animation's name as a blank prop to `AniLink`:
Finalemente, asegurate de proveer el nombre de la animación deseada como una _prop_ _blank_ a `AniLink`:

```javascript
<AniLink paintDrip to="page-4">
  Go to Page 4
</AniLink>
```

Options like transition duration, direction, and more are customizable with props. See [the documentation of AniLink](https://transitionlink.tylerbarnes.ca/docs/anilink/) for more details.
Opciones como duración de la transición, dirección y demás son configurables con _props_. Vé [la documentación de AniLink](https://transitionlink.tylerbarnes.ca/docs/anilink/) para mas detalles.

## Custom transitions
## Transiciones personalizadas

You have two main methods of creating page transitions:
Tienes dos métodos principales de crear transiciones de páginas:

1. Use the `trigger` function defined in your `exit`/`entry` prop. More details in the '[Using the `trigger` function](#using-the-trigger-function)' subsection.
1. Usa la función `trigger` definida en tu _prop_ `exit`/`entry`. Más detalles en la subsección '[Usando la funcion `trigger`](#using-the-trigger-function)'. ==============
2. Use the props passed by `TransitionLink` to define your transitions. More details in the '[Using passed props](#using-passed-props)' subsection.
2. Usa las _props_ pasadas por `TransitionLink` para definir tus transiciones. Más detalles en la subsección '[Usando _props_ pasadas](#using-passed-props)'. ==============

Additionally, you can specify a number of props and options on the `TransitionLink` component, like `length`, `delay`, and more. For more options and details, see [the documentation of TransitionLink](https://transitionlink.tylerbarnes.ca/docs/transitionlink/). For further examples of usage, visit the [plugin's GitHub repository.](https://github.com/TylerBarnes/gatsby-plugin-transition-link)
Adicionalmente, puedes especificar un número de _props_ y opciones en el componente `TransitionLink`, como `length`, `delay` y más. Para mas opciones y detalles, vé [la documentación de TransitionLink](https://transitionlink.tylerbarnes.ca/docs/transitionlink/).

#### Using the trigger function
#### Usando la función trigger

You can specify a `trigger` function that will handle the animation. This is useful for _imperative_ animation libraries like [animejs](https://animejs.com/) or [GSAP](https://greensock.com/gsap) that specify animations with function calls.
Puedes especificar una función `trigger` que manejará la animación. Estas son útiles para las librerías de animaciones _imperativas_ como [animejs](https://animejs.com/) o [GSAP](https://greensock.com/gsap) que especifican animaciones con llamadas a funciones.

```javascript
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

#### Using passed props
#### Usando props pasadas

The exiting and entering pages/templates involved in the transition will receive props indicating the current transition status, as well as the `exit` or `enter` props defined on the `TransitionLink`.
La salida y entrada de páginas/plantillas involucradas en la transición recibiran _props_ indicando el estatus de la transición actual, así como también la _prop_ `exit` o `enter` definida en el `TransitionLink`.


```javascript
const PageOrTemplate = ({ children, transitionStatus, entry, exit }) => {
  console.log(transitionStatus, entry, exit)
  return <div className={transitionStatus}>{children}</div>
}
```

You can combine these props with a _declarative_ state-based animation libraries like [react-pose](https://popmotion.io/pose/) or [react-spring](http://react-spring.surge.sh/) to specify transitions for exiting and entering a page.
Puedes combinar estas _props_ con una librería de animación basada-en-estado _declarativa_ como [react-pose](https://popmotion.io/pose/) o [react-spring](http://react-spring.surge.sh/) para especificar transiciones para salir y entrar a una página.

If you want to access these props in one of your components instead of a page/template, you should wrap your component in the `TransitionState` component. This component takes a function that will have access to the same props as above, which you can then use in your component.
Si quieres acceder a estas _props_ en uno de tus componentes en vez de una página/plantilla, debes envolver tu componente en el componente `TransitionState`. Este componente toma una función que accederá a las mismas propiedades como anteriormente, la cual podras en tu componente.

Here's an example using `TransitionState` and `react-pose` to trigger enter/exit transitions for a `Box` component.
Aquí un ejemplo usando `TransitionState` y `react-pose` para desencadenar las transiciones _enter/exit_ para el componente `Box`.

```javascript
import { TransitionState } from "gatsby-plugin-transition-link"

const Box = posed.div({
  hidden: { opacity: 0 },
  visible: { opacity: 1 },
})

<TransitionState>
      {({ transitionStatus, exit, enter }) => {
        console.log('exit object is', exit)
        console.log('enter object is', enter)

        return (
            <Box
              className="box"
              pose={
                ['entering', 'entered'].includes(transitionStatus)
                  ? 'visible'
                  : 'hidden'
              }
            />
        )
      }}
</TransitionState>
```

Now, the `Box` component will be aware of the transition status of the page it's a child of, and it will fade in/out accordingly.
Ahora, el componente `Box` estará al pendiente del estatus de la transición de la página que es hijo, y aparecera de entrada/salida en consecuencia.

## Excluding elements from page transitions
## Excluyendo elementos de las transiciones de página

You may want to have elements on a page that persist throughout the page transition (_ex. a site-wide header_). This can be accomplished by wrapping elements in the `TransitionPortal` component.
Quizá quieras tener elementos en la página que persistan durante la transición de la página (_ej. una cabecera del ancho-del-sitio_). Esto se puede conseguir envolviendo elementos con el componente `TransitionPortal`.

```javascript
import { TransitionPortal } from "gatsby-plugin-transition-link"
```

```javascript
<TransitionPortal>
  <SomeComponent>
    This component will sit on top of both pages, and persist through page
    transitions.
  </SomeComponent>
</TransitionPortal>
```

As always, check out [the `TransitionPortal` docs](https://transitionlink.tylerbarnes.ca/docs/transitionportal/) for more information about `TransitionPortal`.
Como siempre, checate [los docs `TransitionPortal`](https://transitionlink.tylerbarnes.ca/docs/transitionportal/) para más información acerca de `TransitionPortal`.

## Further reading
## Siguientes lecturas

- [Documentación oficial](https://transitionlink.tylerbarnes.ca/docs/)
- [Código fuente del plugin](https://github.com/TylerBarnes/gatsby-plugin-transition-link)
- [Sitio demo](https://gatsby-plugin-transition-link.netlify.com/)
- [Entrada de blog: 'Per-Link Gatsby page transitions with TransitionLink'](/blog/2018-12-04-per-link-gatsby-page-transitions-with-transitionlink/)
- [Usando transition-link con react-spring](https://github.com/TylerBarnes/gatsby-plugin-transition-link/issues/34)
