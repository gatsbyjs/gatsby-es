---
title: Almacenando en Caché
---

Los plugins pueden almacenar en caché datos en forma de objetos JSON para utilizarlos en compilaciones futuras.

Gatsby ya hace uso del almacenamiento en caché, por ejemplo:

- cualquier nodo creado por los plugins _fuente_ (source) o _transformador_ (transformer) son almacenados en caché
- `gatsby-plugin-sharp` _cachea_ las miniaturas (thumbnails) que se creen

Los datos se almacenan en el directorio `.cache`, que es relativo al directorio raíz de tu proyecto.

## La API caché

La API caché es pasada a [Gatsby's Node APIs](/docs/node-apis/) la cual es usualmente implementada con plugins.

```js
exports.onPostBootstrap = async function({ cache, store, graphql }) {}
```

Las dos funciones que vas a necesitar utilizar son:

### `set`

Establece el valor que se quiere almacenar en caché

`cache.set(key: string, value: any) => Promise<any>`

### `get`

Devuelve el valor _cacheado_

`cache.get(key: string) => Promise<any>`

La documentación que se encuentra en [Node API helpers](/docs/node-api-helpers/#cache) ofrece información más detallada acerca de la API.

## Ejemplo utilizando un plugin

En el archivo del plugin `gatsby-node.js`, puedes acceder al argumento `cache` como se indica a continuación:

```js:title=gatsby-node.js
exports.onPostBuild = async function({ cache, store, graphql }, { query }) {
  const cacheKey = "some-key-name"
  let obj = await cache.get(cacheKey)

  if (!obj) {
    obj = { created: Date.now() }
    const data = await graphql(query)
    obj.data = data
  } else if (Date.now() > obj.lastChecked + 3600000) {
    /* Reload after a day */
    const data = await graphql(query)
    obj.data = data
  }

  obj.lastChecked = Date.now()

  await cache.set(cacheKey, obj)

  /* Do something with data ... */
}
```

## Limpiando el caché

Dado que los archivos caché son guardados dentro del directorio `.cache`, simplemente borrándolo podemos limpiar el mismo. También puedes utilizar la herramienta [`gatsby clean`](/docs/gatsby-cli/#clean) para borrar los directorios `.cache` y `public`.
Puede suceder que Gatsby invalide el caché en algunos casos, más específicamente:

- Si `package.json` es modificado, por ejemplo, si una nueva dependencia es actualizada o agregada
- Si `gatsby-config.js` cambia, por ejemplo, un nuevo plugin es agregado o modificado
- Si `gatsby-node.js` cambia, por ejemplo, si invocas una API Node nueva, o cambia una llamada a `createPage`

## Conclusión

Con la API caché, vas a ser capaz de persistir datos e información entre diferentes compilaciones, lo cual es bastante útil cuando desarrollas un sitio con Gatsby (ya que ejecutas `gatsby develop` muy frecuentemente). Las operaciones que requieren de gran rendimiento (como por ejemplo, transformaciones de imágenes) o la descarga frecuente de datos, pueden presentar una ralentización significativa en el desempeño de Gatsby, por lo cual agregar esta optimización de caché puede resultar en una mejora notable para los usuarios de tu sitio. También puedes echar un vistazo a los siguientes ejemplos que utilizan la API caché: [gatsby-source-contentful](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-source-contentful/src/download-contentful-assets.js), [gatsby-source-shopify](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-source-shopify/src/nodes.js#L23-L54), [gatsby-source-wordpress](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-source-wordpress/src/normalize.js#L471-L537), [gatsby-transformer-remark](https://github.com/gatsbyjs/gatsby/blob/7f5b262d7b5323f1a387b8b7278d9a81ee227258/packages/gatsby-transformer-remark/src/extend-node-type.js), [gatsby-source-tmdb](https://github.com/LekoArts/gatsby-source-tmdb/blob/e12c19af5e7053bfb7737e072db9e24acfa77f49/src/add-local-image.js).
