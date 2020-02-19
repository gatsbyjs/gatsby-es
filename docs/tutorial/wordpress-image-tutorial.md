---
title: "Agregar imágenes a un sitio WordPress"
---

### ¿Qué cubre este tutorial?

En este tutorial, instalarás los diversos plugins y componentes de imagen para extraer los datos de imágenes desde una cuenta de WordPress hacia tu sitio con Gatsby y renderizar dichos datos. Este [demo con Gatsby + WordPress](https://using-wordpress.gatsbyjs.org/sample-post-1) te muestra un ejemplo de lo que estarás construyendo en este tutorial, aunque en este tutorial solo te enfocarás en agregar imágenes.

### ¿Por qué seguir este tutorial?

Las imágenes son una de las formas más hermosas y sorprendentes de comunicarse con las personas, y son una parte clave para crear una experiencia de usuario efectiva y positiva; al mismo tiempo, las imágenes de alta calidad pueden cargar lento y causar que las cajas de texto se muevan, lo que dificulta que las personas sean pacientes cuando visitan tu sitio web.

La Gatsby Way™ de crear imágenes describe un conjunto de buenas prácticas que te ayudan a optimizar el rendimiento y la adaptabilidad de las imágenes para que puedas obtener los beneficios de imágenes increíbles que no hagan lento tu sitio. Este [sitio Gatsbygram](https://gatsbygram.gatsbyjs.org/) (un feed de Instagram alimentado a través de Gatsby) demuestra el efecto de trazado de imágenes svg. Aquí hay un [sitio de demostración de procesamiento de imágenes](https://image-processing.gatsbyjs.org/) que explora como divertirse con imágenes en tu sitio Gatsby.

### Instalación del plugin `gatsby-source-wordpress`

Primero necesitarás instalar el plugin `gatsby-source-wordpress` que tiene imágenes listas para que las uses en tu sitio.

Crea un nuevo proyecto de Gatsby y muévete al directorio del nuevo proyecto que acabas de crear:

```shell
gatsby new images-tutorial-site
cd images-tutorial-site
```

Instala el plugin `gatsby-source-wordpress`. Para obtener más información de las características del plugin y ejemplos de consultas GraphQL que no están incluidas en este tutorial, mira el [archivo README del plugin `gatsby-source-wordpress`](/packages/gatsby-source-wordpress/?=wordpress).

```shell
npm install --save gatsby-source-wordpress
```

Agrega el plugin `gatsby-source-wordpress` a `gatsby-config.js` usando el siguiente código, el cual también lo puedes encontrar en el [código fuente del sitio de ejemplo](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-wordpress/gatsby-config.js).

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Gatsby WordPress Tutorial",
  },
  plugins: [
    // https://public-api.wordpress.com/wp/v2/sites/gatsbyjsexamplewordpress.wordpress.com/pages/
    /*
     * La capa de procesamiento de datos de Gatsby empieza con los plugins
     * de “source”. Aquí el sitio obtiene sus datos desde WordPress.
     */
    // highlight-start
    {
      resolve: `gatsby-source-wordpress`,
      options: {
        /*
         * La URL base del sitio de WordPress sin la barra diagonal y el protocolo. Esto es requerido.
         * Ejemplo : 'dev-gatbsyjswp.pantheonsite.io' o 'www.example-site.com'
         */
        baseUrl: `dev-gatbsyjswp.pantheonsite.io`,
        // El protocolo. Este puede ser http o https.
        protocol: `http`,
        // Indica si el sitio está alojado en wordpress.com.
        // Si es falso, entonces se asume que el sitio es auto alojado.
        // Si es verdadero, entonces el plugin obtendrá su contenido en wordpress.com usando la API REST JSON V2.
        // Si tu sitio está alojado en wordpress.org, configúralo como falso.
        hostingWPCOM: false,
        // Si useACF es verdadero, el plugin fuente intentará importar el contenido del plugin ACF de WordPress.
        // Esta característica no se ha probado para sitios alojados en WordPress.com
        useACF: true,
      },
    },
    // highlight-end
  ],
}
```

### Instalación de plugins para ayuda con las imágenes

Ahora necesitarás agregar los plugins `gatsby-transformer-sharp` y `gatsby-plugin-sharp` a `gatsby-config.js`, agregar una consulta GraphQL a una página, agregar una imagen a la página, y luego visualizar el resultado en el navegador.

Primero, necesitarás instalar algunos plugins y sus dependencias:

```shell
npm install --save gatsby-transformer-sharp gatsby-plugin-sharp gatsby-image
```

Coloca estos plugins en tu `gatsby-config.js` de la siguiente forma:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: "Gatsby WordPress Tutorial",
  },
  plugins: [
    // https://public-api.wordpress.com/wp/v2/sites/gatsbyjsexamplewordpress.wordpress.com/pages/
    /*
     * La capa de procesamiento de datos de Gatsby empieza con los plugins
     * de “source”. Aquí el sitio obtiene sus datos desde WordPress.
     */
    {
      resolve: `gatsby-source-wordpress`,
      options: {
        /*
         * La URL base del sitio de WordPress sin la barra diagonal y el protocolo. Esto es requerido.
         * Ejemplo : 'dev-gatbsyjswp.pantheonsite.io' o 'www.example-site.com'
         */
        baseUrl: `dev-gatbsyjswp.pantheonsite.io`,
        // El protocolo. Este puede ser http o https.
        protocol: `http`,
        // Indica si el sitio está alojado en wordpress.com.
        // Si es falso, entonces se asume que el sitio es auto alojado.
        // Si es verdadero, entonces el plugin obtendrá su contenido en wordpress.com usando la API REST JSON V2.
        // Si tu sitio está alojado en wordpress.org, configúralo como falso.
        hostingWPCOM: false,
        // Si useACF es verdadero, el plugin fuente intentará importar el contenido del plugin ACF de WordPress.
        // Esta característica no se ha probado para sitios alojados en WordPress.com
        useACF: true,
      },
    },
    // highlight-start
    "gatsby-transformer-sharp",
    "gatsby-plugin-sharp",
    // highlight-end
  ],
}
```

### Creación de consultas GraphQL que extraen imágenes de WordPress

Ahora estás listo para crear una consulta GraphQL para extraer algunas imágenes desde el sitio de WordPress.

Ejecuta:

```shell
npm run develop
```

<<<<<<< HEAD
Abre localhost:8000 y localhost:8000/\_\_\_graphql.
=======
Open `http://localhost:8000` and `http://localhost:8000/___graphql`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Aquí hay un ejemplo de creación de anchos y alturas específicas para imágenes:

```graphql
{
  allWordpressPost {
    edges {
      node {
        childWordPressAcfPostPhoto {
          photo {
            localFile {
              childImageSharp {
                # Intenta editar los valores de "width" y "height".
                resolutions(width: 200, height: 200) {
                  # En el explorador de GraphQL, usa los nombres de los campos
                  # como "src". En el código de tu sitio, bórralos
                  # y usa los fragmentos proporcionados por Gatsby.
                  src

                  # Este fragmento no funcionará en el explorador
                  # GraphQL, pero lo puedes usar en tu sitio.
                  # ...GatsbyImageSharpResolutions_withWebp
                }
              }
            }
          }
        }
      }
    }
  }
}
```

Aquí hay una consulta de ejemplo para generar diferentes tamaños de una imagen:

```graphql
{
  allWordpressPost {
    edges {
      node {
        childWordPressAcfPostPhoto {
          photo {
            localFile {
              childImageSharp {
                # Intenta editar el valor de "maxWidth" para generar imágenes redimensionadas.
                fluid(maxWidth: 500) {
                  # En el explorador de GraphQL, usa los nombres de los campos
                  # como "src". En el código de tu sitio, bórralos
                  # y usa los fragmentos proporcionados por Gatsby.
                  src

                  # Este fragmento no funcionará en el explorador
                  # GraphQL, pero lo puedes usar en tu sitio.
                  # ...GatsbyImageSharpFluid_withWebp
                }
              }
            }
          }
        }
      }
    }
  }
}
```

En cualquier caso, puedes agregar soporte para trazado SVG adicionando `_tracedSVG` al final de cada fragmento. _Note esto no funcionará en el explorador GraphQL._

### Renderización de las imágenes en `index.js`

Así es como tu `index.js` debería verse con la consulta agregada:

```jsx:title=src/pages/index.js
import React from "react"
import { graphql, Link } from "gatsby"
import Img from "gatsby-image"

const IndexPage = ({ data }) => {
  const imagesResolutions = data.allWordpressPost.edges.map(
    edge =>
      edge.node.childWordPressAcfPostPhoto.photo.localFile.childImageSharp
        .resolutions
  )
  return (
    <div>
      <h1>Hi people</h1>
      <p>Welcome to your new Gatsby site.</p>
      <p>Now go build something great.</p>
      {imagesResolutions.map(imageRes => (
        <Img resolutions={imageRes} key={imageRes.src} />
      ))}
      <Link to="/page-2/">Go to page 2</Link>
    </div>
  )
}

export default IndexPage

export const query = graphql`
  query {
    allWordpressPost {
      edges {
        node {
          childWordPressAcfPostPhoto {
            photo {
              localFile {
                childImageSharp {
                  # edita el valor de maxWidth para generar imágenes redimensionadas.
                  resolutions(width: 500, height: 500) {
                    ...GatsbyImageSharpResolutions_withWebp_tracedSVG
                  }
                }
              }
            }
          }
        }
      }
    }
  }
`
```

Tu sitio de demostración debería verse así:

![Sitio de ejemplo](./images/wordpress-image-tutorial.gif)

### Probar la velocidad de carga y efectos de tu imagen

Es útil y puede ser divertido enlentecer tu navegador a propósito para ver los efectos de la imagen animarse más lento.

Abre la consola de tu navegador y cambia la velocidad de la red a algo más lento. En Chrome, puedes hacer clic en la pestaña “network”, luego en la flecha desplegable junto a la palabra “Online.” Luego haz clic en “Slow 3G.” Ahora, recarga tu página y mira el difuminado y los efectos SVG en acción. La pestaña de network también muestra estadísticas sobre cuando se cargó cada imagen y cuanto tiempo tomó cargarla.

![Network](./images/network.png)

![Slow 3G](./images/slow-3g.png)
