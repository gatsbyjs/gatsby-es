---
title: Trabajando Con Imágenes En Gatsby
---

La optimización de imágenes es un reto en cualquier página web. Para utilizar las mejores prácticas para rendimiento en dispositvos, necesitas multiples tamaños y resoluciones de cada imagen. Por suerte, Gatsby tiene varios [plugins](/docs/plugins/) útiles que trabajan juntos para hacerlo para imágenes en [componentes de página](/docs/building-with-components/#page-components).

<<<<<<< HEAD
La aproximación recomendada es usar [consultas GraphQL](/docs/querying-with-graphql/) para conseguir imágenes de resolución y tamaño óptimas, y después, mostrarlas con el componente  [`gatsby-image`](/packages/gatsby-image/).
=======
The recommended approach is to use [GraphQL queries](/docs/graphql-concepts/) to get images of the optimal size or resolution, then, display them with the [`gatsby-image`](/packages/gatsby-image/) component.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Consulta Imágenes Con GraphQL

Consultar imágenes con GraphQL te permite acceder a los datos de la imagen tanto como realizar transformaciones con [Sharp](https://github.com/lovell/sharp), una librería de alto rendimiento para el procesamiento de imágenes.

Necesitarás unos cuantos plugins para esto:

<<<<<<< HEAD
- [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) plugin que te permite [consultar archivos con GraphQL](/docs/querying-with-graphql/#images)
- [`gatsby-plugin-sharp`](/packages/gatsby-plugin-sharp) se encarga de las conexiones entre Sharp y los Plugins de Gatsby 
- [`gatsby-transformer-sharp`](/packages/gatsby-transformer-sharp/) te permite crear multiples imágenes de los tamaños adecuados y resoluciones con una consulta

Si la imagen final es de un tamaño fijo, la optimización depende de tener multiples resoluciones de la imagen.  Si es responsiva, es decir, se estira para llenar un contenedor o página, la optimización se basa en tener diferentes tamaños de la misma imagen. Mira la [documentación de `Gatsby Image` para más información](/packages/gatsby-image/#two-types-of-responsive-images).
=======
- [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) plugin allows you to [query files with GraphQL](/docs/graphql-concepts/#images)
- [`gatsby-plugin-sharp`](/packages/gatsby-plugin-sharp) powers the connections between Sharp and Gatsby Plugins
- [`gatsby-transformer-sharp`](/packages/gatsby-transformer-sharp/) allows you to create multiples images of the right sizes and resolutions with a query

If the final image is of a fixed size, optimization relies on having multiple resolutions of the image. If it is responsive, meaning it stretches to fill a container or page, optimization relies on having different sizes of the same image. See the [Gatsby Image documentation for more information](/packages/gatsby-image/#two-types-of-responsive-images).
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

También puedes usar argumentos en tu consulta para especificar exactamente, las dimensiones mínimas, y máximas. Ve la [documentación de `Gatsby Image` para más información](/packages/gatsby-image/#two-types-of-responsive-images).

Este ejemplo es para una galería de imágenes donde las imágenes se estiran cuando se cambia el tamaño de la página. Utiliza el método `fluid` y el fragmento `fluid` para obtener los datos adecuados para usar en el componente `gatsby-image` y argumentos para establecer el ancho como 400px y la altura máxima como 250px.

```js
export const query = graphql`
  query {
    fileName: file(relativePath: { eq: "images/myimage.jpg" }) {
      childImageSharp {
        fluid(maxWidth: 400, maxHeight: 250) {
          ...GatsbyImageSharpFluid
        }
      }
    }
  }
`
```

## Optimizando Imágenes Con Gatsby Image

[`gatsby-image`](/packages/gatsby-image/) es un plugin que automáticamente crea componentes React para imágenes optimizadas que:

> - Carga el tamaño óptimo de imagen para cada tamaño de dispositivo y resolución de pantalla
> - Mantiene la posición de la imagen mientras se carga para que tu página no salte mientras se cargan las imágenes
> - Utiliza el efecto de "desenfoque", es decir, carga una pequeña versión de la imagen para mostrar mientras se carga la imagen completa
> - Alternativamente, proporciona un SVG de "marcador de posición trazado" de la imagen
> - Carga en diferido de imágenes, lo que reduce el ancho de banda y acelera el tiempo de carga inicial
> - Utiliza imágenes [WebP] (https://developers.google.com/speed/webp/), si el navegador admite el formato

Aquí hay un componente de imagen que usa la consulta del ejemplo anterior:

```jsx
<Img fluid={data.fileName.childImageSharp.fluid} alt="" />
```

## Usando Fragmentos Para Estandarizar El Formato

¿Qué pasa si tienes un montón de imágenes y quieres que todas usen el mismo formato?

Un fragmento personalizado es una manera fácil de estandarizar el formato y reutilizarlo en varias imágenes:

```js
export const squareImage = graphql`
  fragment squareImage on File {
    childImageSharp {
      fluid(maxWidth: 200, maxHeight: 200) {
        ...GatsbyImageSharpFluid
      }
    }
  }
`
```

El fragmento puede entonces ser referenciado en la consulta de imagen:

```js
export const query = graphql`
  query {
    image1: file(relativePath: { eq: "images/image1.jpg" }) {
      ...squareImage
    }

    image2: file(relativePath: { eq: "images/image2.jpg" }) {
      ...squareImage
    }

    image3: file(relativePath: { eq: "images/image3.jpg" }) {
      ...squareImage
    }
  }
`
```

### Recursos adicionales

- [Documentación de la API de Gatsby Image ](/docs/gatsby-image/)
- [Usando gatsby-image con Gatsby](https://egghead.io/playlists/using-gatsby-image-with-gatsby-ea85129e)lista de reproducción de egghead.io gratuita
- [README del plugin gatsby-image](/packages/gatsby-image/)
- [gatsby-plugin-sharp archivo README](/packages/gatsby-plugin-sharp/)
- [gatsby-transformer-sharp archivo README](/packages/gatsby-transformer-sharp/)
