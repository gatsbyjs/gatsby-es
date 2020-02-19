---
title: Personalizar html.js
---

<<<<<<< HEAD
Gatsby utiliza un componente React para que el servidor renderize el `<head>` y otras partes
HTML fuera de la aplicación principal de Gatsby. Gatsby también establece un valor predeterminado para la etiqueta `<noscript>` allí.
=======
Gatsby uses a React component to server render the `<head>` and other parts of
the HTML outside of the core Gatsby application.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

La mayoría de los sitios deberían usar el `html.js` predeterminado enviado con Gatsby. Pero si necesitas 
personalizar el html.js de tu sitio, copia el archivo predeterminado en tu 
carpeta de código fuente ejecutando:

```shell
cp .cache/default-html.js src/html.js
```

Y luego haz modificaciones según sea necesario.

Si necesitas insertar html personalizado en el `<head>` o `<footer>` de cada página de tu sitio, puedes usar `html.js`.

<<<<<<< HEAD
### *props* necesarios
=======
> Customizing `html.js` is a workaround solution for when the use of the appropriate APIs is not available in `gatsby-ssr.js`. Consider using [`onRenderBody`](/docs/ssr-apis/#onRenderBody) or [`onPreRenderHTML`](/docs/ssr-apis/#onPreRenderHTML) instead of the method above.
> As a further consideration, customizing `html.js` is not supported within a Gatsby Theme. Use the API methods mentioned instead.

## Required props
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Nota: los diversos *props* que se muestran en las páginas son obligatorios, p. ej.
`headComponents`,`preBodyComponents`, `body` y `postBodyComponents`.

### Insertar html en el `<head>`

Todo lo que renderizas en el componente `html.js` no se hará "de inmediato" en
el cliente como en otros componentes. Si deseas actualizar dinámicamente tu
`<head>` recomendamos usar
[React Helmet](/packages/gatsby-plugin-react-helmet/)

### Insertar html en el `<footer>`

Si desea insertar html personalizado en el pie de página, html.js es la forma preferida de hacerlo. Si estás escribiendo un plugin, considera usar el prop `setPostBodyComponents` en el [Gatsby SSR API](/docs/ssr-apis/).

### Contenedor de destino

Si ves este error: `Uncaught Error: _registerComponent(...): Target container is not a DOM element.` Significa que a tu `html.js` le falta el "contenedor de destino" requerido. 
Dentro de tu `body` debes tener un div con una id de
`___gatsby` como:

```jsx:title=src/html.js
<div
  key={`body`}
  id="___gatsby"
  dangerouslySetInnerHTML={{ __html: this.props.body }}
/>
```

### Agregar JavaScript personalizado

Puedes agregar JavaScript personalizado a tu documento HTML utilizando el atributo React [dangerouslySetInnerHTML](https://reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml).

```jsx:title=src/html.js
<script
  dangerouslySetInnerHTML={{
    __html: `
            var name = 'world';
            console.log('Hello ' + name);
        `,
  }}
/>
```
