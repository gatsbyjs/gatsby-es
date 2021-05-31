---
title: Obteniendo datos desde WordPress
---

Esta guía te ayudará a través del proceso de usar [Gatsby](/) con la [API Rest de WordPress](https://developer.wordpress.org/rest-api/reference/).

WordPress es un gestor de contenidos (CMS) libre y de código abierto. Supongamos que tienes un sitio creado con WordPress y quieres extraer los datos existentes a tu sitio estático en Gatsby. Puedes hacerlo con [gatsby-source-wordpress](/packages/gatsby-source-wordpress/?=wordpress). ¡Empecemos!

_Nota: esta guía usa `gatsby-starter-default` para proporcionarte los conocimientos necesarios para empezar a trabajar con WordPress, pero si te atascas en algún punto siéntete libre de usar
[este ejemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-wordpress) para obtener información adicional._

## Configuración

### Inicio rápido

Esta guía asume que tienes un proyecto Gatsby configurado. Si necesitas configurar un proyecto, dirígete a la [Guía de Inicio Rápido](/docs/quick-start), después vuelve.

### gatsby-config.js

Es esencialmente la base inicial de Gatsby. Las dos cosas definidas aquí inicialmente (en el _starter_) son `siteMetadata` y `plugins` que puedes añadir para habilitar nuevas funcionalidades para tu sitio.

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Starter de Inicio en Gatsby",
  },
  plugins: ["gatsby-plugin-react-helmet"],
  ...
}
```

### Plugin: gatsby-source-wordpress

Ahora que tienes cierta comprensión de la estructura del proyecto, agreguemos la funcionalidad para extraer datos de WordPress. Hay un plugin para ello. [`gatsby-source-wordpress`](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-source-wordpress) es el plugin de Gatsby para obtener datos desde sitios WordPress usando la JSON REST API. Puedes instalarlo ejecutando el siguiente comando:

```shell
npm install gatsby-source-wordpress
```

### Configurando el plugin

En `gatsby-config.js`, añade tus opciones de configuración, incluyendo la baseUrl y protocolo de tu sitio WordPress, si está alojado en [wordpress.com](http://wordpress.com/) o auto alojado, y si usa el plugin Advanced Custom Fields (ACF) o no.

```javascript:title=gatsby-config.js
module.exports = {
  ...
  plugins: [
    ...,
    {
      resolve: `gatsby-source-wordpress`,
      options: {
        // el origen de tu WordPress
        baseUrl: `wpejemplo.com`,
        protocol: `https`,
        // ¿si está alojado en wordpress.com, o auto alojado?
        hostingWPCOM: false,
        // ¿usa tu sitio el plugin Advanced Custom Fields?
        useACF: false
      }
    },
  ]
}
```

**Nota**: Si tu configuración varía de lo que se muestra arriba, por ejemplo, si estás alojando tu instancia WordPress en WordPress.com, por favor consulta los [documentos del plugin](/packages/gatsby-source-wordpress/?=wordpre#how-to-use) para más información de cómo configurar otras opciones requeridas para tu caso de uso.

## Usando datos de WordPress

Una vez que tu plugin fuente está extrayendo datos, puedes construir las páginas de tu sitio implementando la API `createPages` en `gatsby-node.js`. Cuando esto es llamado, tus datos ya han sido extraídos y están disponibles para ser consultados con GraphQL. Gatsby usa [GraphQL al momento del build](/docs/graphql-concepts/#how-does-graphql-and-gatsby-work-together); Tu plugin fuente (en este caso, `gatsby-source-wordpress`) obtiene tu información, y Gatsby usa esos datos para "[automáticamente _inferir_ un esquema GraphQL](/docs/graphql-concepts/#how-does-graphql-and-gatsby-work-together)" contra la que puedas consultar.

La API `createPages` expone la función `graphql`:

> La función GraphQL nos permite ejecutar consultas arbitrarias contra el esquema local de WordPress... como si el sitio tuviera una base de datos incluida construida a partir los datos recuperados contra los que puedes realizar consultas. ([Fuente](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-wordpress/gatsby-node.js#L15))

Puedes usar el archivo [`gatsby-node.js`](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-wordpress/gatsby-node.js) de la demo del plugin para empezar. Para los fines de esta guía, el código para construir entradas funciona de forma predeterminada. Consulta tu esquema GraphQL local de WordPress para todas las entradas, [itera a través de cada nodo de las Entradas](/docs/programmatically-create-pages-from-data/) y crea una página estática para cada una, [basado en la plantilla definida](/docs/layout-components/).

Por ejemplo, aquí abajo tienes un extracto de ejemplo en `gatsby-node.js`.

```javascript:title=gatsby-node.js
const path = require(`path`);
const { slash } = require(`gatsby-core-utils`);

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions;

  // consulta contenido para entradas de WordPress
  const result = await graphql(`
    query {
      allWordpressPost {
        edges {
          node {
            id
            slug
          }
        }
      }
    }
  `);

  const postTemplate = path.resolve(`./src/templates/post.js`);
  result.data.allWordpressPost.edges.forEach(edge => {
    createPage({
      // será la url de tu página
      path: edge.node.slug,
      // especifica un componente de plantilla a tu elección
      component: slash(postTemplate),
      // En la consulta GraphQL de la plantilla, 'id' estará disponible
      // como una variable GraphQL para realizar consultas de datos de esta entrada.
      context: {
        id: edge.node.id
      }
    });
  });
};
```

Después de obtener los datos desde WordPress a través de la consulta, todas las entradas se iteran, llamando a [`createPage`](/docs/actions/#createPage) para cada una.

Una [página de Gatsby es definida](/docs/api-specification/#concepts) como "una página del sitio con un nombre de ruta, un componente de plantilla, y una consulta de GraphQL y componente _Layout opcionales_."

Cuando reinicies tu servidor con el comando `gatsby develop` podrás navegar a las nuevas páginas creadas para cada una de tus entradas en sus respectivas rutas.

En el IDE GraphiQL en `localhost:8000/__graphql` deberías ver ahora campos consultables para `allWordpressPosts` en la barra lateral de documentos o del explorador.

## Terminando

Este fue un ejemplo muy básico para ayudarte a entender cómo obtener datos desde WordPress y usarlos con Gatsby. Como
la guía ya ha mencionado, si te atascas, puedes echar un vistazo al
[repositorio de ejemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-wordpress), que es un ejemplo funcional
creado para dar soporte a esta guía.

## Otros recursos

- [Publicación en la que se basa esta guía](/blog/2018-01-22-getting-started-gatsby-and-wordpress/)
- [Video tutoriales "Watch + Learn"](http://watch-learn.com/series/gatsbyjs-wordpress)
- [Otra publicación sobre el uso de Gatsby con WordPress](https://indigotree.co.uk/how-use-wordpress-headless-cms/)
- Más [Publicaciones en el blog de Gatsby sobre Gatsby + WordPress](/blog/tags/wordpress/)
