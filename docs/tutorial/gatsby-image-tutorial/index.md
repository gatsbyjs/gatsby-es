---
title: Usando Gatsby-Image En Su Sitio
---

## ¿Qué contiene este tutorial?

Al finalizar este tutorial, habrá hecho lo siguiente:

- aprendido cómo usar `gatsby-image` para imágenes adaptables
- obtenido una sóla imágen con GraphQL
- obtenido múltiples imágenes mediante archivos YAML
- aprendido cómo solucionar errores comunes

## Prerequisitos

Este tutorial asume que ya tiene un proyecto con Gatsby en marcha y funcionado así como imágenes que le gustaría renderizar en su página. Para configurar un sitio con Gatsby, revise el [tutorial principal](/tutorial/) ó la [guía de inicio rápido](/docs/quick-start/).

En este tutorial aprenderá cómo configurar `gatsby-image`, un componente de React que optimiza imágenes adaptables usando GraphQL y la capa de datos de Gatsby. Será informado de una serie de maneras de usar `gatsby-image`, y algunas trampas.

> _Nota: este tutorial usa ejemplos de contenido estático almacenado en archivos YAML, pero métodos parecidos pueden ser usados para archivos Markdown._

## Empezando

La optimización de imágenes en Gatsby la realiza un plugin llamado `gatsby-image` que es increiblemente eficiente.

### Paso 1

Comienzae usando npm para instalar el plugin `gatsby-image` y sus dependencias asociadas.

```bash
npm install gatsby-image gatsby-transformer-sharp gatsby-plugin-sharp
```

### Paso 2

Añada los nuevos plugins instalados a su archivo `gatsby-config.js`. El archivo de configuración se parecerá a algo así (otros plugins en uso se han eliminado de este código para simplificarlo).

> _Nota: una vez que `gatsby-image` se ha instalado, no es necesario incluirlo en el archivo `gatsby-config.js`._

```javascript:title=gatsby-config.js
plugins: [`gatsby-transformer-sharp`, `gatsby-plugin-sharp`]
```

## Configuración de Gatsby-image

Ahora está listo para usar `gatsby-image`.

### Paso 3

Determine dónde están localizados sus archivos de imagen. En este ejemplo están en `src/data`.

Si aún no lo ha hecho, asegúrese de que su proyecto está configurado para ver contenido dentro de ese directorio. Esto significa dos cosas:

1.  Instale `gatsby-source-filesystem`. Nota: Si creó su proyecto usando `gatsby new <name>`, este primer paso ya debería estar realizado via el "starter" predeterminado.

```bash
npm install gatsby-source-filesystem
```

2. El siguiente paso es asegurarse que en su archivo `gatsby-config.js` se especifíca el directorio correcto. En este ejemplo se vería así:

```javascript:title=gatsby-config.js
plugins: [
  `gatsby-transformer-sharp`,
  `gatsby-plugin-sharp`,
  { resolve: `gatsby-source-filesystem`, options: { path: `./src/data/` } },
]
```

¡Ahora ya puede empezar a trabajar con `gatsby-image`!

## Paso 4

El siguiente paso puede variar dependiendo de lo que quiera conseguir.

## Consultar datos de una sola imagen

Usw `graphql` para consultar un archivo de imagen directamente. Puede incluir la ruta relativa a su archivo de imagen y determinar cómo quiere que `gatsby-image` procese su archivo.

```jsx:title=src/pages/index.js
export const query = graphql`
  query {
    file(relativePath: { eq: "headers/headshot.jpg" }) {
      childImageSharp {
        fixed(width: 125, height: 125) {
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`
```

Hay un par de cosas a tener en cuenta aquí.

### Rutas relativas de imagen y `gatsby-config.js`

Puede esperar que la ruta relativa sea relativa al archivo donde se encuentra el código, en este caso index.js. Sin embargo, esto no funciona. La ruta relativa se basa realmente en la línea de código que indique en la configuración de `gatsby-source-filesystem`, que apunta a `src/data`.

### Fragmentos de imagen

Otra cosa a tener en cuenta sobre esa consulta es cómo usa el fragmento `GatsbyImageSharpFixed` para devolver una imagen de ancho y alto fijos. También podría usar el fragmento `GatsbyImageSharpFluid` que genera imágenes escalables que llenan su contenedor en vez de ajustarse a dimensiones específicas. En `gatsby-image`, imágenes _fluid_ están destinadas a imágenes que no tienen un tamaño determinado dependiendo de la pantalla, mientras que otras son _fixed_.

La consulta devolverá un objeto de datos que incluye la imagen procesada en un formato utilizable para el componente `gatsby-image`. El resultado devuelto será pasado automáticamente al componente y se adjuntará a la propiedad `data`. Luego puede mostrar la imagen usando JSX para generar automáticamente HTML adaptable y de alto rendimiento.

Para mostrar la imagen, empiece por importar el componente proporcionado por `gatsby-image`.

```jsx
import Img from "gatsby-image"
```

Ahora puede usarlo. Tenga en cuenta que la _key_ para apuntar a la imagen corresponde al modo en el que la imagen se procesó. En este ejemplo es `fixed`.

```jsx
<Img
  className="headshot"
  fixed={data.file.childImageSharp.fixed}
  alt="headshot"
/>
```
Esta es una consulta y su uso todo en conjunto:

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import Img from "gatsby-image"
import Layout from "../components/layout"

const HomePage = ({ data }) => {
  return (
    <Layout>
      <Img
        className="headshot"
        fixed={data.file.childImageSharp.fixed}
        alt=""
      />
    </Layout>
  )
}

export const query = graphql`
  query {
    file(relativePath: { eq: "headers/headshot.jpg" }) {
      childImageSharp {
        fixed(width: 125, height: 125) {
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`
export default HomePage
```

## Consultando múltiples imágenes desde datos YAML

Otra manera de obtener imágenes es a través de YAML (o Markdown). Este ejemplo usa el plugin `gatsby-transformer-yaml` para consultar archivos YAML. Más información sobre este plugin se puede encontrar en la [librería de plugins de Gatsby](/packages/gatsby-transformer-yaml/?=gatsby-transformer-yaml).

Aquí un ejemplo de una consulta de una lista de conferencias en un archivo YAML con una imagen para cada una:

```graphql
{
  allSpeakingYaml {
    edges {
      node {
        conference
        year
        image {
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
}
```

En este caso la consulta empieza con `allSpeakingYaml` para dirigir a `graphql` a buscar esta información en el archivo `speaking.yaml` de su directorio `src/data` referenciado en `gatsby-config.js`. Si quiere consultar un archivo llamado `blog.yaml`, por ejemplo, comenzaría la consulta con `allBlogYaml`.

## Renderizando imágenes obtenenidas de YAML

Para hacer referencia a sus imágenes en YAML, asegúrese de que las rutas relativas sean correctas. La ruta para cada imagen debe ser relativa a la localización a la que se apunte en el archivo `.yaml`. Y todos esos archivos deben estar en un directorio visible para el plugin `gatsby-source-filesystem` configurado en `gatsby-config.js`.

El interior del archivo YAML se vería así:

```
- image: speaking/kcdc.jpg
```

Ahora, puede crear la consulta. Al igual que en el ejemplo anterior de una sola imagen, puede usar las funciones de `gatsby-image` dentro de la consulta. Cuando la consulta se ejecute, la ruta relativa apuntará a la ubicación del archivo de imagen y la consulta resultante procesará el archivo como una imagen a mostrar.

```graphql
{
  allSpeakingYaml {
    edges {
      node {
        image {
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
}
```
Debido a que las imágenes se almacenan como parte de un _array_, se puede acceder a ellas usando la función JavaScript `map` en JSX. Como en el ejemplo de una sola imagen, la imagen procesada está en el nivel `...GatsbyImageSharpFluid` en la estructura de datos resultante.

```jsx
<Img
  className="selfie"
  fluid={node.image.childImageSharp.fluid}
  alt={node.conference}
/>
```

## Usando la consulta Static

Si su consulta es parte de un componente reutilizable, es posible que quiera usar el _hook_ `useStaticQuery`. El código necesario para hacer esto es casi el mismo que en el caso anterior de imagen única.

```javascript:title=src/components/header-image.js
export default () => {
  const data = useStaticQuery(graphql`
    query {
      file(relativePath: { eq: "headers/default.jpg" }) {
        childImageSharp {
          fixed(width: 125, height: 125) {
            ...GatsbyImageSharpFixed
          }
        }
      }
    }
  `)

  return <Img fixed={data.file.childImageSharp.fixed} />
}
```

En vez de una consulta de constante y datos que hacen referencia al resultado como en la primera sección anterior, puede colocar el _hook_ `useStaticQuery` directamente en el código JSX y luego referenciarlo en el componente `Img`. Tenga en cuenta que ni el código de la consulta ni la sintaxis de la etiqueta `Img` cambiaron; el único cambio fue la ubicación de la consulta y el uso de la función `useStaticQuery` para envolverla.


## Múltiples consultas y alias

El último caso de uso que puede encontrar es cómo manejar una situación donde tiene múltiples consultas en el mismo archivo/página.

Este ejemplo está intentando consultar todos los datos en `speaking.yaml` y la consulta de archivo directa en nuestro primer ejemplo. Para hacer esto, puedes usar un alias en GraphQL.

La primera cosa a saber es que un alias asigna un nombre a una consulta. La segunda cosa a saber es que un alias es opcional, pero puede hacer su vida más fácil. A continuación, un ejemplo.

```graphql
talks: allSpeakingYaml {
        edges {
            node {
                image {
                    childImageSharp {
                        fluid {
                            ...GatsbyImageSharpFluid
                        }
                    }
                }
            }
        }
    }
}
```

Cuando haga esto, ha cambiado la referencia al objeto de consulta disponible en su código JSX. Mientras anteriormente se le hizo referencia como aquí:

```jsx
{
  data.allSpeakingYaml.edges.map(({ node }) => (
    <Img fluid={node.image.childImageSharp.fluid} alt={node.alt} />
  ))
}
```

Darle un alias no añade un nivel de complejidad al objeto de respuesta, solo lo reemplaza. Entonces termina con la misma estructura, referenciada así (ten en cuenta el alias `talk` en lugar del más largo` allSpeakingYaml`):

```jsx
{
  data.talks.edges.map(({ node }) => (
    <Img fluid={node.image.childImageSharp.fluid} alt={node.alt} />
  ))
}
```

El nombre del objeto de nivel superior `data` está implícito. Esto es importante porque cuando realice múltiples consultas como parte de un solo componente, Gatsby aún pasa el resultado completo al componente.

Aquí hay un ejemplo de datos que se incluye en un componente:

```jsx
const SpeakingPage = ({ data }) => {}
```

Todo lo demás se referencia desde ese nombre de retorno de nivel superior.

Sabiendo esto, puede combinar dos consultas que hacen referencia a imágenes y usar alias para distinguir entre ellas.

```graphql
{
  allSpeakingYaml {
    edges {
      node {
        image {
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
  banner: file(relativePath: { eq: "headers/default.jpg" }) {
    childImageSharp {
      fluid {
        ...GatsbyImageSharpFluid
      }
    }
  }
}
```

Tenga en cuenta que este ejemplo usa alias para una consulta y no para la otra. Esto está permitido; no es necesario que todas sus consultas utilicen alias. En este caso, el JSX se vería así para acceder al contenido en `speaking.yaml`.


```jsx
{
  data.allSpeakingYaml.edges.map(({ node }) => (
    <Img fluid={node.image.childImageSharp.fluid} alt={node.alt} />
  ))
}
```

Y luego así para acceder a la imagen usando el alias `banner`.

```jsx
<Img fluid={data.banner.childImageSharp.fluid} />
```

Estos ejemplos deberían servir para un buena cantidad de casos de uso. Un par de cosas extra:

## Relación de aspecto

`gatsby-image` tiene una característica que le permite establecer una relación de aspecto para restringir las proporciones de la imagen. Esto se puede usar tanto en imágenes procesadas fijas como fluidas; no importa.

```jsx
<Img sizes={{ ...data.banner.childImageSharp.fluid, aspectRatio: 21 / 9 }} />
```

Este ejemplo usa la opción `sizes` en el componente `Img` para especificar la opción `aspectRatio` junto con los datos de la imagen fluida. Este procesamiento es posible gracias a `gatsby-plugin-sharp`.

## Consejo extra: Error

Ahora los errores a tener en cuenta. Si cambia el procesamiento de su imagen de `fixed` a `fluid`, es posible que vea este error.

![Mensaje de error: inImageCache](./ErrorMessage.png)

A pesar de su apariencia, resolver esto realmente no require vaciar ningún tipo de caché. En realidad, tiene que ver con referencias incompatibles. Probablemente se lanzó el error porque cambió la consulta para procesarla como `fluid` pero la _key_ en el JSX todavía estaba configurada como `fixed`, o vice versa.

## Fin

Eso es todo. Este tutorial incluyó una serie de posibles casos de uso, así que no sienta que necesita explorarlos todos. Elija los ejemplos y consejos que se aplican a su implementación.

## Otros recursos

- [Documentos de la API de imagen de Gatsby](/docs/gatsby-image/)
- [Usando imagen de Gatsby](/docs/using-gatsby-image/)
- [Otras técnicas de imagen y medios en Gatsby](/docs/images-and-files/)
