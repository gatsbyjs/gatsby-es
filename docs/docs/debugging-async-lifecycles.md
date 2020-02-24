---
title: Depuración de métodos de ciclo de vida asíncrono
---

Se presume que varios métodos de ciclo de vida (consulta: [Gatsby Node APIs](/docs/node-apis/)) dentro de Gatsby son asíncronos. En otras palabras, estos métodos pueden _eventualmente_ resolverse en un valor y este valor es una [`Promesa`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Esperamos a que se resuelva la `Promesa`, y luego marcamos el método de ciclo de vida como completado cuando lo hace.

En el contexto de Gatsby, esto significa que si estás invocando una funcionalidad asincrónica (por ejemplo, solicitudes de datos, llamadas `graphql`, etc.) y no se devuelve correctamente la Promesa, puede surgir un problema interno donde el resultado de esas llamadas ocurre _después_ que el método de ciclo de vida ya se ha marcado como completado. Consideremos un ejemplo:

```js:title=gatsby-node.js
exports.createPages = async function({ actions, graphql }) {
  // highlight-start
  graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `).then(res => {
    res.data.allMarkdownRemark.edges.forEach(edge => {
      const slug = edge.node.fields.slug
      actions.createPage({
        path: slug,
        component: require.resolve(`./src/templates/post.js`),
        context: { slug },
      })
    })
  })
  // highlight-end
}
```

¿Puedes detectar el error? En este caso, se invocó una acción asincrónica (`graphql`) pero esta acción asincrónica no fue `devuelta` ni `esperada` desde `createPages`. Esto significa que el método de ciclo de vida se marcará como completo antes de que se complete, lo que lleva a errores de datos faltantes y otros errores difíciles de depurar.

La solución es sorprendentemente simple: ¡solo se debe cambiar una línea!

```js:title=gatsby-node.js
exports.createPages = async function({ actions, graphql }) {
  // highlight-next-line
  await graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `).then(res => {
    res.data.allMarkdownRemark.edges.forEach(edge => {
      const slug = edge.node.fields.slug
      actions.createPage({
        path: slug,
        component: require.resolve(`./src/templates/post.js`),
        context: { slug },
      })
    })
  })
}
```

## Mejores prácticas

### Usa `async` / `await`

Con Node 8, Node puede interpretar de forma nativa las funciones `async`. ¡Esto te permite escribir código asincrónico como si fuera síncrono! ¡Esto puede limpiar el código que anteriormente usaba una cadena `Promise` y tiende a ser un poco más simple de entender!

### Usa `Promise.all` si es necesario

[`Promise.all`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) wraps up _multiple_ asynchronous actions and resolves when _each_ have completed. This can be especially helpful if you're pulling from multiple data sources or abstracted some code that returns a Promise into a helper. For instance, consider the following code:

```js:title=gatsby-node.js
const fetch = require("node-fetch")

const getJSON = uri => fetch(uri).then(response => response.json())

exports.createPages = async function({ actions, graphql }) {
  // highlight-start
  const [pokemonData, rickAndMortyData] = await Promise.all([
    getJSON("https://some-rest-api.com/pokemon"),
    getJSON("https://some-rest-api.com/rick-and-morty"),
  ])
  // highlight-end

  // use data to create pages with actions.createPage
}
```
