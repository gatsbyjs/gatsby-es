---
title: Obteniendo datos desde el sistema de archivos
---

Esta guía te ayudará con la obtención de datos del sistema de archivos.

## Configuración

Esta guía asume que tienes un proyecto Gatsby configurado. Si necesitas configurar un proyecto, dirígete a la [Guía de Inicio Rápido](/docs/quick-start).

También será útil si estás familiarizado con [GraphiQL](/docs/introducing-graphiql/), una herramienta que te ayuda a estructurar tus consultas correctamente.

## Usando `gatsby-source-filesystem`

`gatsby-source-filesystem` es el plugin de Gatsby para crear nodos `File` desde el sistema de archivos.

Instala el plugin desde la raíz de tu proyecto Gatsby:

```shell
npm install --save gatsby-source-filesystem
```

Después añádelo al archivo `gatsby-config.js` de tu proyecto:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `El Nombre de tu Sitio`,
  },
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    // highlight-end
  ],
}
```

Guarda el archivo `gatsby-config.js`, y reinicia el servidor de desarrollo de Gatsby.

Abre GraphiQL.

Si abres la ventana de autocompletar, verás:

![graphiql-filesystem](./images/graphiql-filesystem.png)

Pulsa <kbd>Enter</kbd> en `allFile` después pulsa <kbd>Ctrl + Enter</kbd> para ejecutar una
consulta.

![filesystem-query](./images/filesystem-query.png)

Borra el `id` de la consulta y vuelve a abrir el autocompletado (<kbd>Ctrl +
Espacio</kbd>).

![filesystem-autocomplete](./images/filesystem-autocomplete.png)

Intenta añadir una serie de campos a tu consulta, pulsando <kbd>Ctrl + Enter</kbd>
cada vez para re-ejecutar la consulta. Verás algo parecido a esto:

![allfile-query](./images/allfile-query.png)

El resultado es un _array_ de "nodos" `File` (nodo es un nombre elegante para un objeto en un
"grafo"). Cada objeto `File` tiene los campos que has consultado.

<<<<<<< HEAD
## Transformando nodos `File`
=======
If you have multiple sets of data, you can query specific ones by specifying the `name` property from the config object in the `gatsby-config.js` file. In this case, `name` is set to `src`.

```javascript:title=gatsby-config.js
{
  resolve: `gatsby-source-filesystem`,
  options: {
    path: `${__dirname}/src`,
    name: `src`,
  },
},
```

You can then update your query using `sourceInstanceName` and the value of the `name` property in a filter like so.

```graphql
{
  allFile(filter: { sourceInstanceName: { eq: "src" } }) {
    edges {
      node {
        relativePath
        prettySize
        extension
        birthTime
      }
    }
  }
}
```

## Transforming File nodes
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Una vez que los archivos se han obtenido, varios plugins "transformadores" en el ecosistema Gatsby pueden ser usados para transformar los nodos `File` en otros varios tipos de datos. Por ejemplo, un archivo JSON puede ser obtenido usando `gatsby-source-filesystem`, y luego los nodos `File` resultates pueden ser transformados en nodos JSON usando `gatsby-transformer-json`.

## Más referencias y ejemplos

Para más referencia, puedes estar interesado en revisar el [README del paquete](/packages/gatsby-source-filesystem/) de `gatsby-source-filesystem`, y varios [starters que usan el plugin](/starters/?d=gatsby-source-filesystem) tanto oficiales como de la comunidad.