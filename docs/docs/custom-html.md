---
title: Personalizar html.js
---

Gatsby utiliza un componente React para que el servidor renderize el `<head>` y otras partes
HTML fuera de la aplicación principal de Gatsby. Gatsby también establece un valor predeterminado para la etiqueta `<noscript>` allí.

La mayoría de los sitios deberían usar el `html.js` predeterminado enviado con Gatsby. Pero si necesitas 
personalizar el html.js de tu sitio, copia el archivo predeterminado en tu 
carpeta de código fuente ejecutando:

```shell
cp .cache/default-html.js src/html.js
```

Y luego haz modificaciones según sea necesario.

Si necesitas insertar html personalizado en el `<head>` o `<footer>` de cada página en su sitio, puedes usar `html.js`.

### *props* necesarios

Nota: los diversos *props* que se muestran en las páginas son obligatorios, p. ej.
`headComponents`,`preBodyComponents`, `body` y `postBodyComponents`.

### Insertar html en el `<head>`

Todo lo que renderizas en el componente `html.js` no se hará "live" en
el cliente como otros componentes le gustan otros componentes. Si deseas actualizar dinámicamente tu
`<head>` recomendamos usar
[React Helmet](/packages/gatsby-plugin-react-helmet/)

### Insertar html en el `<footer>`

Si desea insertar html personalizado en el pie de página, html.js es la forma preferida de hacerlo. Si está escribiendo un complemento, considere usar el accesorio `setPostBodyComponents` en la [Gatsby SSR API](/docs/ssr-apis/).

### Contenedor de destino

Si ves este error: `Uncaught Error: _registerComponent(...): Target container is not a DOM element.`
significa que a tu `html.js` le falta el "contenedor de destino"
requerido. Dentro de tu `body` debes tener un div con una id de
`___ gatsby` como:

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
