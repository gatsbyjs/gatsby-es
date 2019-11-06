---
title: Obtener Datos del Cliente
---

## Contexto

Este artículo trata sobre cómo obtener datos tanto en tiempo de _compilación_ como en tiempo de _ejecución_. Se usa el plugin [`gatsby-source-graphql`](/packages/gatsby-source-graphql/) para obtener datos [durante la compilación](/docs/glossary#build) en el servidor, mientras que usa el paquete [`axios`](https://github.com/axios/axios) para obtener diferentes datos en el [lado del cliente](/docs/glossary#client-side) cuando se carga la página.

Cuando este artículo mencione [hidratación](/docs/glossary#hydration), significa que Gatsby (a través de React.js) crea archivos estáticos para hacer _server-side rendering_ (renderizado en el servidor). Cuando el paquete de secuencias de comandos de Gatsby se descarga y ejecuta en el navegador, se conserva el markup HTML creado por Gatsby y convierte el sitio en una aplicación web React completa que puede manipular el [DOM](/docs/glossary#dom). El resultado de este proceso crea páginas de carga rápida y una experiencia de usuario grata.

Compilar páginas durante el [tiempo de compilación](/docs/glossary#build) es útil cuando el contenido de tu sitio web no cambia con frecuencia, o cuando el proceso de recompilación es simple. Sin embargo, algunos sitios web con necesidades más dinámicas requieren una [ejecución](/docs/glossary#runtime) en el [lado del cliente](/docs/glossary#client-side) para manejar el contenido que cambia constantemente después de que se carga la página, como un widget de chat o una aplicación web de cliente de correo electrónico.

## Combinando datos de compilación y ejecución en el lado del cliente

Debido a que un sitio de Gatsby se [hidrata](/docs/glossary#hydration) en una aplicación React después de cargarse estáticamente, Gatsby no es solo para sitios estáticos. También puedes obtener datos dinámicamente en el lado del cliente según sea necesario, como lo harías con cualquier otra aplicación React.

Para ilustrar esto, usaremos un pequeño sitio de ejemplo que utiliza la capa de datos de Gatsby en el momento de la compilación y los datos del cliente en el tiempo de ejecución. Este ejemplo se basa libremente en el ejemplo del sitio [Gatsby con Apollo](https://github.com/jlengstorf/gatsby-with-apollo) de Jason Lengstorf. Tu obtendrás datos de personajes para Rick (de Rick y Morty) y una imagen aleatoria de cachorros.

> Nota: Revisa el [ejemplo completo aquí](https://github.com/amberleyromo/gatsby-client-data-fetching), si te es de más ayuda.

### 1. Crea un componente de página de Gatsby

Sin datos aún. Sólo la página básica React en donde agregarás los datos.

```jsx:title=index.js
import React, { Component } from "react";
import { graphql } from "gatsby";

class EjemploDeObtencionDesdeCliente extends Component {
  render() {
    return (
      <div style={{ textAlign: "center", width: "600px", margin: "50px auto" }}>
        <h1>Imagen de Rick</h1>
        <p>Esto se obtendrá en una query durante la compilación</p>

        <h2>Imagen de la mascota de Rick</h2>
        <p>Esto se obtendrá en una solicitud del cliente</p>
      </div>
      );
    }
  }

export default ClientFetchingExample;
```

### 2. Obtén la información del personaje al momento de compilación

Para obtener la información y la imagen del personaje de Rick, utiliza el plugin `gatsby-source-graphql`. Esto te permitirá consultar la API de Rick y Morty utilizando consultas de Gatsby.

> Nota: Para aprender más acerca de cómo usar [`gatsby-source-graphql`](/packages/gatsby-source-graphql/), o acerca de la [Capa de datos GraphQL de Gatsby](/docs/graphql/), echa un vistazo a sus respectivos documentos. El propósito de incluirlos aquí es solo para comparación.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-source-graphql",
      options: {
        typeName: "RMAPI",
        fieldName: "rickAndMorty",
        url: "https://rickandmortyapi-gql.now.sh/",
      },
    },
  ],
}
```

Ahora puedes agregar la consulta a tu página `index.js`:

```jsx:title=index.js
import React, { Component } from "react"
import { graphql } from "gatsby"

// highlight-start
// Esta query es ejecutada al momento de compilación de Gatsby.
export const GatsbyQuery = graphql`
  {
    rickAndMorty {
      character(id: 1) {
        name
        image
      }
    }
  }
`
// highlight-end

class EjemploDeObtencionDesdeCliente extends Component {
    render() {
        // highlight-start
        const {
            rickAndMorty: { character }
        } = this.props.data;
        // highlight-end

        return (
          <div style={{ textAlign: "center", width: "600px", margin: "50px auto" }}>
            // highlight-start
            <h1>{character.name} Con Su Mascota</h1>
            <p>Los datos de la API de Rick & Morty se obtienen al momento de compilación.</p>
            <div>
              <img
                src={character.image}
                alt={character.name}
                style={{ width: 300 }}
              />
            </div>
            // highlight-end
            <h2>Imagen de la mascota de Rick</h2>
            <p>Esto se obtendrá desde una solicidud del cliente</p>
          </div>
        )
    }
}

export default EjemploDeObtencionDesdeCliente;
```

### 3. Obtén la información de la mascota y los datos de la imagen en el cliente

Para finalizar, obtendrás la información de mascotas desde la [API Dog de CEO Dog](https://dog.ceo/dog-api/). (Eligirás un cachorro al azar. Rick no es quisquilloso.)

```jsx:title=index.js
import React, { Component } from "react"
import { graphql } from "gatsby"
import axios from "axios" // highlight-line

// Esta query es ejecutada al momento de compilación de Gatsby.
export const GatsbyQuery = graphql`
  {
    rickAndMorty {
      character(id: 1) {
        name
        image
      }
    }
  }
`

class EjemploDeObtencionDesdeCliente extends Component {
  // highlight-start
  state = {
    cargando: false,
    error: false,
    mascota: {
      img: "",
      raza: "",
    },
  }
  // highlight-end

  // highlight-start
  componentDidMount() {
    this.obtenMascotaDeRick()
  }
  // highlight-end

  render() {
    const {
      rickAndMorty: { character },
    } = this.props.data

    const { img, raza } = this.state.mascota // highlight-line

    return (
      <div style={{ textAlign: "center", width: "600px", margin: "50px auto" }}>
        <h1>{character.name} Con Su Mascota</h1>
        <p>Los datos de la API de Rick & Morty se obtienen al momento de compilación.</p>
        <p>Los datos de la API de Dog se cargan al tiempo de ejecución.</p> // highlight-line
        <div>
          <img
            src={character.image}
            alt={character.name}
            style={{ width: 300 }}
          />
        </div>
         {/* highlight-start */}
        <div>
          {this.state.cargando ? (
            <p>Un momento por favor, ¡mascota en camino!</p>
          ) : img && raza ? (
            <>
              <h2>{`¡La mascota es un ${raza}!`}</h2>
              <img src={img} alt={`mono aleatorio `} style={{ maxWidth: 300 }} />
            </>
          ) : (
            <p>Oh no, error obteniendo la mascota :(</p>
          )}
        </div>
       </div> {/* highlight-end */}
    )
  }

  // Estos datos se obtienen al momento de ejecución en el cliente. // highlight-start
  obtenMascotaDeRick = () => {
    this.setState({ cargando: true })

    axios
      .get(`https://dog.ceo/api/breeds/image/random`)
      .then(mascota => {
        const {
          data: { message: img },
        } = mascota
        const raza = img.split("/")[4]

        this.setState({
          cargando: false,
          mascota: {
            ...this.state.mascota,
            img,
            raza,
          },
        })
      })
      .catch(error => {
        this.setState({ cargando: false, error })
      })
  }
} // highlight-end

export default EjemploDeObtencionDesdeCliente
```

Eso es todo -- un ejemplo de consulta de datos en tiempo de compilación utilizando la capa de datos Gatsby GraphQL y solicitando datos dinámicamente en el cliente en tiempo de ejecución.

## Otros recursos

Puede que te interese consultar otros proyectos (tanto utilizados en producción como pruebas de conceptos) que ilustran este uso:

- [Tienda de Gatsby](https://github.com/gatsbyjs/store.gatsbyjs.org)
- [Correo de Gatsby](https://github.com/DSchau/gatsby-mail)
