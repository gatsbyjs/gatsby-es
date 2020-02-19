---
title: Usando Gatsby-Image En Tu Sitio
---

## ¿Qué contiene este tutorial?

Al finalizar este tutorial, habrás hecho lo siguiente:

- aprendido cómo usar `gatsby-image` para imágenes adaptables
- obtenido una sóla imagen con GraphQL
- obtenido múltiples imágenes mediante archivos YAML
- aprendido cómo solucionar errores comunes

## Prerequisitos

Este tutorial asume que ya tienes un proyecto con Gatsby en marcha y funcionado así como imágenes que te gustaría renderizar en tu página. Para configurar un sitio con Gatsby, revisa el [tutorial principal](/tutorial/) ó la [guía de inicio rápido](/docs/quick-start/).

En este tutorial aprenderás cómo configurar `gatsby-image`, un componente de React que optimiza imágenes adaptables usando GraphQL y la capa de datos de Gatsby. Serás informado de una serie de maneras de usar `gatsby-image`, y algunas trampas.

> _Nota: este tutorial usa ejemplos de contenido estático almacenado en archivos YAML, pero métodos parecidos pueden ser usados para archivos Markdown._

## Empezando

La optimización de imágenes en Gatsby la realiza un plugin llamado `gatsby-image` que es increíblemente eficiente.

### Paso 1

Comienza usando npm para instalar el plugin `gatsby-image` y sus dependencias asociadas.

```bash
npm install gatsby-image gatsby-transformer-sharp gatsby-plugin-sharp
```

### Paso 2

Añade los nuevos plugins instalados a tu archivo `gatsby-config.js`. El archivo de configuración se parecerá a algo así (otros plugins en uso se han eliminado de este código para simplificarlo).

> _Nota: una vez que `gatsby-image` se ha instalado, no es necesario incluirlo en el archivo `gatsby-config.js`._

```javascript:title=gatsby-config.js
plugins: [`gatsby-transformer-sharp`, `gatsby-plugin-sharp`]
```

## Configuración de Gatsby-image

Ahora estás listo para usar `gatsby-image`.

### Paso 3

Determina dónde están localizados tus archivos de imagen. En este ejemplo están en `src/data`.

Si aún no lo has hecho, asegúrate de que tu proyecto está configurado para ver contenido dentro de ese directorio. Esto significa dos cosas:

1.  Instala `gatsby-source-filesystem`. Nota: Si creaste tu proyecto usando `gatsby new <name>`, este primer paso ya debería estar realizado vía el "starter" predeterminado.

```bash
npm install gatsby-source-filesystem
```

2. El siguiente paso es asegurarte que en tu archivo `gatsby-config.js` se especifica el directorio correcto. En este ejemplo se vería así:

```javascript:title=gatsby-config.js
plugins: [
  `gatsby-transformer-sharp`,
  `gatsby-plugin-sharp`,
  { resolve: `gatsby-source-filesystem`, options: { path: `./src/data/` } },
]
```

¡Ahora ya puedes empezar a trabajar con `gatsby-image`!

## Paso 4

El siguiente paso puede variar dependiendo de lo que quieras conseguir.

## Consultar datos de una sola imagen

Usa `graphql` para consultar un archivo de imagen directamente. Puedes incluir la ruta relativa a tu archivo de imagen y determinar cómo quieres que `gatsby-image` procese tu archivo.

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

Puedes esperar que la ruta relativa sea relativa al archivo donde se encuentra el código, en este caso index.js. Sin embargo, esto no funciona. La ruta relativa se basa realmente en la línea de código que indiques en la configuración de `gatsby-source-filesystem`, que apunta a `src/data`.

### Fragmentos de imagen

Otra cosa a tener en cuenta sobre esa consulta es cómo usa el fragmento `GatsbyImageSharpFixed` para devolver una imagen de ancho y alto fijos. También podrías usar el fragmento `GatsbyImageSharpFluid` que genera imágenes escalables que llenan su contenedor en vez de ajustarse a dimensiones específicas. En `gatsby-image`, imágenes _fluid_ están destinadas a imágenes que no tienen un tamaño determinado dependiendo de la pantalla, mientras que las otras son _fixed_.

La consulta devolverá un objeto de datos que incluye la imagen procesada en un formato utilizable para el componente `gatsby-image`. El resultado devuelto será pasado automáticamente al componente y se adjuntará a la propiedad `data`. Luego puedes mostrar la imagen usando JSX para generar automáticamente HTML adaptable y de alto rendimiento.

Para mostrar la imagen, empieza por importar el componente proporcionado por `gatsby-image`.

```jsx
import Img from "gatsby-image"
```

Ahora puedes usarlo. Ten en cuenta que la _key_ para apuntar a la imagen corresponde al modo en el que la imagen se procesó. En este ejemplo es `fixed`.

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

En este caso la consulta empieza con `allSpeakingYaml` para dirigir a `graphql` a buscar esta información en el archivo `speaking.yaml` de tu directorio `src/data` referenciado en `gatsby-config.js`. Si quieres consultar un archivo llamado `blog.yaml`, por ejemplo, comenzarías la consulta con `allBlogYaml`.

## Renderizando imágenes obtenenidas de YAML

Para hacer referencia a tus imágenes en YAML, asegúrate de que las rutas relativas sean correctas. La ruta para cada imagen debe ser relativa a la localización a la que se apunte en el archivo `.yaml`. Y todos esos archivos deben estar en un directorio visible para el plugin `gatsby-source-filesystem` configurado en `gatsby-config.js`.

El interior del archivo YAML se vería así:

```yaml
- image: speaking/kcdc.jpg
```

Ahora, puedes crear la consulta. Al igual que en el ejemplo anterior de una sola imagen, puedes usar las funciones de `gatsby-image` dentro de la consulta. Cuando la consulta se ejecute, la ruta relativa apuntará a la ubicación del archivo de imagen y la consulta resultante procesará el archivo como una imagen a mostrar.

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

Si tu consulta es parte de un componente reutilizable, es posible que quieras usar el _hook_ `useStaticQuery`. El código necesario para hacer esto es casi el mismo que en el caso anterior de imagen única.

```jsx:title=src/components/header-image.js
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

En vez de una consulta de constante y datos que hacen referencia al resultado como en la primera sección anterior, puedes colocar el _hook_ `useStaticQuery` directamente en el código JSX y luego referenciarlo en el componente `Img`. Ten en cuenta que ni el código de la consulta ni la sintaxis de la etiqueta `Img` cambiaron; el único cambio fue la ubicación de la consulta y el uso de la función `useStaticQuery` para envolverla.

El último caso de uso que puedes encontrar es cómo manejar una situación donde tienes múltiples consultas en el mismo archivo/página.

## Múltiples consultas y alias

Este ejemplo está intentando consultar todos los datos en `speaking.yaml` y la consulta de archivo directa en nuestro primer ejemplo. Para hacer esto, puedes usar un alias en GraphQL.

La primera cosa a saber es que un alias asigna un nombre a una consulta. La segunda cosa a saber es que un alias es opcional, pero puede hacer tu vida más fácil. A continuación, un ejemplo.

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

Cuando hagas esto, has cambiado la referencia al objeto de consulta disponible en tu código JSX. Mientras anteriormente se le hizo referencia como aquí:

```jsx
{
  data.allSpeakingYaml.edges.map(({ node }) => (
    <Img fluid={node.image.childImageSharp.fluid} alt={node.alt} />
  ))
}
```

Darle un alias no añade un nivel de complejidad al objeto de respuesta, solo lo reemplaza. Entonces terminas con la misma estructura, referenciada así (ten en cuenta el alias `talk` en lugar del más largo` allSpeakingYaml`):

```jsx
{
  data.talks.edges.map(({ node }) => (
    <Img fluid={node.image.childImageSharp.fluid} alt={node.alt} />
  ))
}
```

El nombre del objeto de nivel superior `data` está implícito. Esto es importante porque cuando realices múltiples consultas como parte de un solo componente, Gatsby aún pasa el resultado completo al componente.

Aquí hay un ejemplo de datos que se incluye en un componente:

```jsx
const SpeakingPage = ({ data }) => {}
```

Todo lo demás se referencia desde ese nombre de retorno de nivel superior.

Sabiendo esto, puedes combinar dos consultas que hacen referencia a imágenes y usar alias para distinguir entre ellas.

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

Ten en cuenta que este ejemplo usa alias para una consulta y no para la otra. Esto está permitido; no es necesario que todas tus consultas utilicen alias. En este caso, el JSX se vería así para acceder al contenido en `speaking.yaml`.

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

Ahora los errores a tener en cuenta. Si cambias el procesamiento de tu imagen de `fixed` a `fluid`, es posible que veas este error.

![Mensaje de error: inImageCache](./ErrorMessage.png)

A pesar de su apariencia, resolver esto realmente no require vaciar ningún tipo de caché. En realidad, tiene que ver con referencias incompatibles. Probablemente se lanzó el error porque cambiaste la consulta para procesarla como `fluid` pero la _key_ en el JSX todavía estaba configurada como `fixed`, o vice versa.

## Fin

Eso es todo. Este tutorial incluyó una serie de posibles casos de uso, así que no sientas que necesitas explorarlos todos. Elije los ejemplos y consejos que se aplican a tu implementación.

## Otros recursos

- [Documentos de la API de Gatsby Image](/docs/gatsby-image/)
- [Usando imagen de Gatsby](/docs/using-gatsby-image/)
- [Otras técnicas de imagen y medios en Gatsby](/docs/images-and-files/)
