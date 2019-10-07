---
título: Personalizar html.js
---

Gatsby utiliza un componente React para que el servidor procese el `<head>` y otras partes de
el HTML fuera de la aplicación principal de Gatsby. Gatsby también establece un valor predeterminado para la etiqueta `<noscript>` allí.

La mayoría de los sitios deberían usar el `html.js` predeterminado enviado con Gatsby. Pero si necesitas
para personalizar el html.js de su sitio, copie el predeterminado en su fuente
árbol corriendo:

```shell
cp .cache/default-html.js src/html.js
```

Y luego haga modificaciones según sea necesario.

Si necesita insertar html personalizado en el `<head>` o `<footer>` de cada página en su sitio, puede usar `html.js`.

### *props* necesarios

Nota: los diversos *props* que se muestran en las páginas son obligatorios, p.
`headComponents`,`preBodyComponents`, `body` y `postBodyComponents`.

### Insertar html en el `<head>`

Todo lo que renderizado en el componente `html.js` no se hará "live "en
Al cliente le gustan otros componentes. Si desea actualizar dinámicamente su
`<head>` recomendamos usar
[React Helmet](/packages/gatsby-plugin-react-helmet/)

### Insertar html en el `<footer>`

Si desea insertar html personalizado en el pie de página, html.js es la forma preferida de hacerlo. Si está escribiendo un complemento, considere usar el accesorio `setPostBodyComponents` en la [Gatsby SSR API](/docs/ssr-apis/).

### Contenedor de destino

Si ve este error: `Uncaught Error: _registerComponent(...): Target container is not a DOM element.`
significa que a su `html.js` le falta el requerido
"contenedor de destino". Dentro de su `body` debe tener un div con una id de
`___ gatsby` como:

```jsx:title=src/html.js
<div
  key={`body`}
  id="___gatsby"
  dangerouslySetInnerHTML={{ __html: this.props.body }}
/>
```

### Agregar JavaScript personalizado

Puede agregar JavaScript personalizado a su documento HTML utilizando el atributo React [dangerouslySetInnerHTML](https://reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml).

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
