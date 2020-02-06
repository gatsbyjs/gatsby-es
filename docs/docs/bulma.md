---
title: Bulma
---

[Bulma](https://bulma.io) es gratis, es un framework CSS de código abierto basado en Flexbox. Esta guía le mostrará cómo comenzar con Gatsby y Bulma.

Esta guía asume que tiene un proyecto Gatsby configurado. Si necesita configurar un proyecto, diríjase a [**Guía de inicio rápido**](/docs/quick-start), luego regrese.

### Instalación

Para empezar, instalemos todos los paquetes que vamos a necesitar.

`yarn add bulma node-sass gatsby-plugin-sass`

Luego agregue el `gatsby-plugin-sass` en `gatsby-config.js`.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

### Archivo para estilos

Ahora es el momento de crear un archivo scss que contenga nuestro estilo personalizado y la declaración de importación para bulma.

(Para simplificar las cosas, inserte el archivo al lado de index.js en el pages-directory)

```scss:title=mystyles.scss
@charset "utf-8";

// If need, change your variables before importing Bulma
$title-color: #ff0000;

@import "~bulma/bulma.sass";
```

### Utilizar Bulma

El último paso es importar el estilo y usarlo.

Reemplacemos el contenido predeterminado del archivo index.js.

```javascript:title=index.js
import React from "react"
import "./mystyles.scss"

const IndexPage = () => {
  return (
    <div className="container">
      <div className="columns">
        <div className="column">
          <h2 className="title is-2">Level 2 heading</h2>
          <p className="content">Cool content. Using Bulma!</p>
        </div>

        <div className="column is-four-fifths">
          <h2 className="title is-2">Level 2 heading</h2>
          <p className="content">This column is cool too!</p>
        </div>
      </div>
    </div>
  )
}

export default IndexPage
```

¡Y eso es todo! Ahora puedes usar Bulma como lo harías normalmente.

### Recursos

- [Documentación de Bulma sobre cómo usar sass](https://bulma.io/documentation/customize/with-node-sass/)
