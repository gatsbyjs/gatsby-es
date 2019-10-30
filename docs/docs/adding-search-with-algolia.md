---
title: Añadiendo un buscador con Algolia
---

Una vez que hayas añadido contenido a tu sitio, querrás que tus visitantes encuentren fácilmente lo que están buscando. Esta guía te llevará por el proceso de configurar un experiencia de búsqueda personalizada, soportada por [Algolia](https://www.algolia.com), en cualquier sitio desarrollado con Gatsby. Escribirás componentes funcionales que dependen de _Hooks_ de React, así que, para seguir esta guía, se requiere que uses [React 16.8](https://reactjs.org/blog/2019/02/06/react-v16.8.0) o superior.

Es importante que sepas estas dos cosas antes de que empieces:

1. Además de esta guía, también pudieras consultar la extensa [documentación de Algolia sobre cómo iniciar con React](https://www.algolia.com/doc/guides/building-search-ui/getting-started/react).
2. Si estás buscando añadir un buscador a un sitio de documentación, puedes dejar que Algolia haga la mayoría de pasos indicados abajo usando su funcionalidad [Docsearch](https://community.algolia.com/docsearch). Para sitios de otros tipos y un fino control sobre qué datos exactos deben ser indexados, sigue leyendo.

## ¿Por qué usar Algolia?

Algolia es una plataforma de alojamiento de buscadores que aloja información del índice de páginas por ti, y retorna los resultados en donde sea que esté la búsqueda de tu sitio. Tú le dices a Algolia qué paginas tienes, dónde están y cómo navegar hacia ellas, y Algolia te devuelve esos resultados basada en cualquier término de búsqueda usado.

Para implementar la búsqueda de Algolia en un sitio Gatsby, tendrás que instalar el _plugin_, decirle qué información consultar, proveer tus credenciales de Algolia, y seguir otros pocos pasos de configuración. Esto significa que después de que las consultas se hayan ejecutado cuando haces un `gatsby build`, Algolia tendrá disponible el índice entero de tu sitio y podrá devolver resultados a usuarios rápidamente. Para aprender más acerca de los beneficios de usar Algolia, [revisa este post en el blog de Netlify, quienes recientemente cambiaron el buscador de su sitio al de Algolia](https://www.netlify.com/blog/2017/10/10/replacing-our-search-with-algolia/).

## Configuración del _plugin_ de Algolia

En primer lugar, necesitarás añadir [`gatsby-plugin-algolia`](https://github.com/algolia/gatsby-plugin-algolia) y [`react-instantsearch-dom`](https://github.com/algolia/react-instantsearch) a tu proyecto. `react-instantsearch` es la librería de Algolia que contiene componentes React disponibles, los cuales puedes importar para ahorrarte un montón de trabajo. También usarás `dotenv` el cual viene con Gatsby por defecto. Necesitarás especificar tu _app ID_ de Algolia y las _API keys_ de búsqueda y administración sin agregarlas a tu sistema de control de versiones.

```shell
npm install --save gatsby-plugin-algolia react-instantsearch-dom algoliasearch dotenv
```

En esta guía usarás `styled-components` para diseñar la interfaz de usuario de la búsqueda pero puedes usar cualquier otra solución de CSS que prefieras. Si también eliges usar `styled-components`, deberás instalarlo.

```shell
npm install --save styled-components gatsby-plugin-styled-components
```

Luego, añade `gatsby-plugin-algolia` y `gatsby-plugin-styled-components` a tu `gatsby-config.js`.

```js:title=gatsby-config.js
const queries = require("./src/utils/algolia")

require("dotenv").config()

module.exports = {
  siteMetadata: {
    title: `Gatsby+Algolia`,
    description: `Cómo configurar la búsqueda de Algolia en Gatsby`,
    author: `<tu nombre>`,
  },
  plugins: [
    {
      resolve: `gatsby-plugin-algolia`,
      options: {
        appId: process.env.GATSBY_ALGOLIA_APP_ID,
        apiKey: process.env.ALGOLIA_ADMIN_KEY,
        queries,
        chunkSize: 10000, // default: 1000
      },
    },
    `gatsby-plugin-styled-components`,
  ],
}
```

Nota que estás obteniendo `queries` desde un archivo en `./src/utils/algolia.js` (por su puesto que podrías ponerlo donde desees) y tu _ID de Algolia_ y _API key_ desde `.env`. Así que, creemos esos archivos.

Para esto, necesitas navegar a [la sección 'API Keys' de tu perfil de Algolia](https://www.algolia.com/api-keys). Si ya tienes una cuenta, encontrarás tus _API keys_ ahí. Si no la tienes, necesitarás crear una y luego navegar a ese enlace. Deberá verse como esta captura de pantalla, con la diferencia de que tendrá información real, no como ahora que veremos información redactada a manera de ejemplo:

![captura de pantalla de api key de algolia](./images/algolia-api-keys.png)

Una vez que tengas tu _App ID_, _Search-Only API Key_ y _Admin API Key_, coloca el siguiente código en tu archivo `.env`, reemplazando la información ficticia con tus llaves reales:

```text:title=.env
GATSBY_ALGOLIA_APP_ID=KA4OJA9KAS
GATSBY_ALGOLIA_SEARCH_KEY=lkjas987ef923ohli9asj213k12n59ad
ALGOLIA_ADMIN_KEY=lksa09sadkj1230asd09dfvj12309ajl
```

Las _keys_ en el código de ejemplo anterior son secuencias de caracteres randómicos, pero las que copies desde tu perfil de Algolia deberán tener la misma longitud. Uno de los beneficios de usar este método para consultar tus _API keys_ es que todas son guardadas en un solo archivo en el servidor, y por lo tanto, nunca son expuestas al lado del cliente, lo cual incrementa la seguridad.

Como tu archivo .env contiene tus _API keys_ reales y privadas, es considerado un riesgo de seguridad hacer _commit_ de tu archivo `.env`. Es una buena práctica hacer _commit_ a git o a cualquier otro sistema de control de versiones de un archivo `.env.example`, así se sabrá qué variables de entorno se deben proveer, sin mostrar tus _keys_ privadas.

```text:title=.env.example
# renombre este archivo como .env y provee los valores listados abajo
# también asegúrate de que esté disponible para herramientas de compilación (ej: Netlify)
# advertencia: las variables con el prefijo GATSBY_ serán accesibles desde código del lado del cliente
# se cuidadoso de no exponer información sensible (en este caso tu 'admin API key' de Algolia)

GATSBY_ALGOLIA_APP_ID=ingreseValor
GATSBY_ALGOLIA_SEARCH_KEY=ingreseValor
ALGOLIA_ADMIN_KEY=ingreseValor
```

Las consultas o `queries` (en inglés) te permiten obtener la información que quieras que Algolia indexe directamente desde la capa de GraphQL de Gatsby, exportándolas desde `src/utils/algolia.js` como un arreglo de objetos. Cada objeto está formado por una consulta GraphQL obligatoria y un nombre de índice opcional, una función transformadora (_transformer function_) y un objeto de configuraciones (_settings_).

```js:title=src/utils/algolia.js
const pageQuery = `{
  pages: allMarkdownRemark(
    filter: {
      fileAbsolutePath: { regex: "/pages/" },
      frontmatter: {purpose: {eq: "page"}}
    }
  ) {
    edges {
      node {
        objectID: id
        frontmatter {
          title
          slug
        }
        excerpt(pruneLength: 5000)
      }
    }
  }
}`

const postQuery = `{
  posts: allMarkdownRemark(
    filter: { fileAbsolutePath: { regex: "/posts/" } }
  ) {
    edges {
      node {
        objectID: id
        frontmatter {
          title
          slug
          date(formatString: "MMM D, YYYY")
          tags
        }
        excerpt(pruneLength: 5000)
      }
    }
  }
}`

const flatten = arr =>
  arr.map(({ node: { frontmatter, ...rest } }) => ({
    ...frontmatter,
    ...rest,
  }))
const settings = { attributesToSnippet: [`excerpt:20`] }

const queries = [
  {
    query: pageQuery,
    transformer: ({ data }) => flatten(data.pages.edges),
    indexName: `Pages`,
    settings,
  },
  {
    query: postQuery,
    transformer: ({ data }) => flatten(data.posts.edges),
    indexName: `Posts`,
    settings,
  },
]

module.exports = queries
```

Tal vez se vea un poco intimidante al inicio, pero solamente estás haciéndole saber a `gatsby-plugin-algolia` cómo obtener la información con la cual llenará tus índices en sus servidores. El ejemplo de arriba usa consultas separadas pasando datos a índices separados de páginas y posts del blog.

Los _transformers_ te permiten modificar los datos retornados por las consultas para convertirlos a un formato listo para la búsqueda. Lo que estás haciendo aquí es poner a un mismo nivel los atributos de posts y páginas para _'desanidar'_ los campos de _frontmatter_ (como `author`, `date`, `tags`) pero los _transformers_ pueden hacer mucho más si lo necesitas. Esto hace el proceso de indexado de información bastante flexible y poderoso. Podríamos, por ejemplo, usarlos para filtrar los resultados de tus consultas, formatear campos, añadir otros, unirlos, etc.

Si has llegado hasta aquí entonces el _"backend"_ está listo. Deberías poder ejecutar `gatsby build` y ver tus índices en la interface web de Algolia llenos con tus datos.

## Añadir una interfaz de búsqueda a tu sitio

Ahora, vamos a construir una interfaz de búsqueda para el usuario de nuestro sitio. Necesitamos una manera en la que el usuario pueda ingresar una cadena a buscar, enviar esta cadena a Algolia, recibir de los índices los resultados que coincidan con el criterio de búsqueda (llamados _hits_ en lenguaje de Algolia) y finalmente mostrar esos resultados al usuario. Empecemos.

Vamos a montar todo lo que necesitas en un componente de React llamado `Search` que llamarás desde cualquier parte de tu sitio en el que quieras que el usuario pueda realizar una búsqueda. Aunque el diseño varíe bastante de un sitio a otro, se revisará en esta guía los estilos implementados con [`styled-components`](https://styled-components.com) debido a que me tomó algún tiempo hacer que funcionen las transiciones CSS para que la caja de búsqueda se deslice cuando el usuario haga clic sobre ella y mostrar los resultados una vez que Algolia retorne las coincidencias.

El componente `Search` está formado por los siguientes archivos:

- **`index.js`**: el componente principal
- **`input.js`**: el campo de texto
- **`hitComps.js`**: los componentes que renderizarán las páginas/posts que coincidan con el criterio de búsqueda
- **`styles.js`**: los componentes estilizados

Están sucediendo algunas cosas en estos archivos, así que vamos a descomponerlos uno por uno, pieza por pieza.

### `index.js`

```js:title=src/components/search/index.js
import React, { useState, useEffect, createRef } from "react"
import {
  InstantSearch,
  Index,
  Hits,
  connectStateResults,
} from "react-instantsearch-dom"
import algoliasearch from "algoliasearch/lite"

import { Root, HitsWrapper, PoweredBy } from "./styles"
import Input from "./Input"
import * as hitComps from "./hitComps"

const Results = connectStateResults(
  ({ searchState: state, searchResults: res, children }) =>
    res && res.nbHits > 0 ? children : `No results for '${state.query}'`
)

const Stats = connectStateResults(
  ({ searchResults: res }) =>
    res && res.nbHits > 0 && `${res.nbHits} result${res.nbHits > 1 ? `s` : ``}`
)

const useClickOutside = (ref, handler, events) => {
  if (!events) events = [`mousedown`, `touchstart`]
  const detectClickOutside = event =>
    !ref.current.contains(event.target) && handler()
  useEffect(() => {
    for (const event of events)
      document.addEventListener(event, detectClickOutside)
    return () => {
      for (const event of events)
        document.removeEventListener(event, detectClickOutside)
    }
  })
}

export default function Search({ indices, collapse, hitsAsGrid }) {
  const ref = createRef()
  const [query, setQuery] = useState(``)
  const [focus, setFocus] = useState(false)
  const searchClient = algoliasearch(
    process.env.GATSBY_ALGOLIA_APP_ID,
    process.env.GATSBY_ALGOLIA_SEARCH_KEY
  )
  useClickOutside(ref, () => setFocus(false))
  return (
    <InstantSearch
      searchClient={searchClient}
      indexName={indices[0].name}
      onSearchStateChange={({ query }) => setQuery(query)}
      root={{ Root, props: { ref } }}
    >
      <Input onFocus={() => setFocus(true)} {...{ collapse, focus }} />
      <HitsWrapper show={query.length > 0 && focus} asGrid={hitsAsGrid}>
        {indices.map(({ name, title, hitComp }) => (
          <Index key={name} indexName={name}>
            <header>
              <h3>{title}</h3>
              <Stats />
            </header>
            <Results>
              <Hits hitComponent={hitComps[hitComp](() => setFocus(false))} />
            </Results>
          </Index>
        ))}
        <PoweredBy />
      </HitsWrapper>
    </InstantSearch>
  )
}
```

En la parte superior, importas `InstantSearch` de [`react-instantsearch-dom`](https://community.algolia.com/react-instantsearch) el cual es el componente raíz que permite conectar toda tu experiencia de búsqueda con el servicio de Algolia. Como el nombre lo indica, `Index` te permite acceder a un índice individual y `Hits` te provee de la información retornada, relacionada a la búsqueda del usuario. Finalmente [`connectStateResults`](https://community.algolia.com/react-instantsearch/connectors/connectStateResults.html) envuelve a componentes personalizados de React y los provee con estadísticas de alto nivel sobre la búsqueda actual como: la consulta, el número de resultados y cuánto tiempo tomó obtenerlas.

Luego importas los componentes estilizados que componen la interfaz de usuario y el componente `Input` en el cual el usuario ingresa la consulta.

```js:title=src/components/search/index.js
import { Root, SearchBox, HitsWrapper, PoweredBy } from "./styles"
import Input from "./Input"
```

`PoweredBy` renderiza la cadena "Powered by Algolia" con un pequeño logo y link. Si estás usando la generosa cuenta gratuita de Algolia, ellos te piden que los menciones de esta manera debajo de los resultados de búsqueda. `react-instantsearch-dom` también provee un [componente de `PoweredBy`](https://community.algolia.com/react-instantsearch/widgets/PoweredBy.html) específicamente para este propósito, pero yo prefiero construir el mío. Regresaremos a estos componentes estilizados una vez que hayamos terminado con `index.js`. Por ahora, continuemos.

Lo último que necesitas para que el componente `Search` funcione, es usar componentes _hit_ para cada tipo de resultado que quieres mostrar al usuario. El componente _hit_ determina cómo los atributos de los resultados (como autor, fecha, etiquetas y título en el caso del post del blog) son mostrados al usuario.

```js:title=src/components/search/index.js
import * as hitComps from "./hitComps"
```

A continuación definirás dos componentes conectados. `Results` informará al usuario que no se encontraron coincidencias para la consulta, a menos que, el número de _hits_ sea positivo, es decir, si `searchResults.nbHits > 0`. `Stats` mostrará `searchResults.nbHits`.

```js:title=src/components/search/index.js
const Results = connectStateResults(
  ({ searchState: state, searchResults: res, children }) =>
    res && res.nbHits > 0 ? children : `No results for ${state.query}`
)

const Stats = connectStateResults(
  ({ searchResults: res }) =>
    res && res.nbHits > 0 && `${res.nbHits} result${res.nbHits > 1 ? `s` : ``}`
)
```

Ahora trabajaremos en el verdadero componente de búsqueda `Search`. Este empieza con algunas inicializaciones de estados, definiciones de funciones para manejar eventos. Todo lo que hace este código es deslizar hacia afuera el cuadro de texto de la búsqueda cuando el usuario hace clic en el ícono de buscar y lo desaparece de nuevo cuando el usuario hace clic o toca la pantalla(en móviles) en otra parte.

```js:title=src/components/search/index.js
export default function Search({ indices, collapse, hitsAsGrid }) {
  const ref = createRef()
  const [query, setQuery] = useState(``)
  const [focus, setFocus] = useState(false)
  const searchClient = algoliasearch(
    process.env.GATSBY_ALGOLIA_APP_ID,
    process.env.GATSBY_ALGOLIA_SEARCH_KEY
  )

  const handleClickOutside = event =>
    !ref.current.contains(event.target) && setFocus(false)

  useEffect(() => {
    [`mousedown`, `touchstart`].forEach(event =>
      document.addEventListener(event, handleClickOutside)
    )
    return () =>
      [`mousedown`, `touchstart`].forEach(event =>
        document.removeEventListener(event, handleClickOutside)
      )
  })
```

`Search` devuelve JSX que renderiza un arreglo dinámico de `indices` pasados como _prop_. Cada ítem del arreglo debe ser un objeto con llaves como `name`, `title`, `hitComp`. El `name` especifica el índice a ser consultado en tu cuenta de Algolia, el `title` es el título a mostrar encima de los resultados que verá el usuario y `hitComp` el componente _hit_ que renderiza los datos devueltos por cada coincidencia.

```js:title=src/components/search/index.js
  return (
    <InstantSearch
      searchClient={searchClient}
      indexName={indices[0].name}
      onSearchStateChange={({ query }) => setQuery(query)}
      root={{ Root, props: { ref } }}
    >
      <Input onFocus={() => setFocus(true)} {...{ collapse, focus }} />
      <HitsWrapper show={query.length > 0 && focus} asGrid={hitsAsGrid}>
        {indices.map(({ name, title, hitComp }) => (
          <Index key={name} indexName={name}>
            <header>
              <h3>{title}</h3>
              <Stats />
            </header>
            <Results>
              <Hits hitComponent={hitComps[hitComp](() => setFocus(false))} />
            </Results>
          </Index>
        ))}
        <PoweredBy />
      </HitsWrapper>
    </InstantSearch>
  )
}
```

Pasar este arreglo de `indices` como un prop, permite reusar el mismo componente de búsqueda `Search` en diferentes partes del sitio y además permite que cada uno de ellos consulte diferentes índices. Por ejemplo, aparte de tener una caja de búsqueda principal en la cabecera del sitio para encontrar páginas y/o posts, tal vez quisieras tener una wiki en tu sitio y ofrecer a tus visitantes una segunda caja de búsqueda que muestre solo resultados de la wiki.

Nota que usaste el mismo _app ID_ en `algoliasearch` que especificaste en el archivo `.env` y que fue usado también en `src/utils/algolia.js` así como tu _search-only API key_ para generar una búsqueda en el cliente que conecta con tu _backend_. _¡No copies tu admin API key de Algolia aquí!_ `algoliasearch` solo necesita _leer_ tus índices. Pegar tu _admin key_ aquí permitirá que otros la obtengan cuando tu sitio sea desplegado. Y alguien podría empezar a meterse en tus datos indexados en Algolia.

## `input.js`

```js:title=src/components/search/input.js
import React from "react"
import { connectSearchBox } from "react-instantsearch-dom"

import { SearchIcon, Form, Input } from "./styles"

export default connectSearchBox(({ refine, ...rest }) => (
  <Form>
    <Input
      type="text"
      placeholder="Search"
      aria-label="Search"
      onChange={e => refine(e.target.value)}
      {...rest}
    />
    <SearchIcon />
  </Form>
))
```

El componente `Input` es donde el usuario ingresa la cadena de búsqueda. Este es relativamente corto ya que el trabajo duro es realizado por Algolia en la función [`connectSearchBox`](https://community.algolia.com/react-instantsearch/connectors/connectSearchBox.html).

Ahora, vamos a echar un vistazo a los componentes estilizados `SearchIcon`, `Form`, `Input` así como a los que han sido importados en `index.js`.

## `styles.js`

```js:title=src/components/search/styles.js
import React from "react"
import styled, { css } from "styled-components"
import { Search } from "styled-icons/fa-solid/Search"
import { Algolia } from "styled-icons/fa-brands/Algolia"

export const Root = styled.div`
  position: relative;
  display: grid;
  grid-gap: 1em;
`

export const SearchIcon = styled(Search)`
  width: 1em;
  pointer-events: none;
`

const focus = css`
  background: white;
  color: ${props => props.theme.darkBlue};
  cursor: text;
  width: 5em;
  + ${SearchIcon} {
    color: ${props => props.theme.darkBlue};
    margin: 0.3em;
  }
`

const collapse = css`
  width: 0;
  cursor: pointer;
  color: ${props => props.theme.lightBlue};
  + ${SearchIcon} {
    color: white;
  }
  ${props => props.focus && focus}
  margin-left: ${props => (props.focus ? `-1.6em` : `-1em`)};
  padding-left: ${props => (props.focus ? `1.6em` : `1em`)};
  ::placeholder {
    color: ${props => props.theme.gray};
  }
`

const expand = css`
  background: ${props => props.theme.veryLightGray};
  width: 6em;
  margin-left: -1.6em;
  padding-left: 1.6em;
  + ${SearchIcon} {
    margin: 0.3em;
  }
`

export const Input = styled.input`
  outline: none;
  border: none;
  font-size: 1em;
  background: transparent;
  transition: ${props => props.theme.shortTrans};
  border-radius: ${props => props.theme.smallBorderRadius};
  {hightlight-next-line}
  ${props => (props.collapse ? collapse : expand)};
`

export const Form = styled.form`
  display: flex;
  flex-direction: row-reverse;
  align-items: center;
`

export const HitsWrapper = styled.div`
  display: ${props => (props.show ? `grid` : `none`)};
  max-height: 80vh;
  overflow: scroll;
  z-index: 2;
  -webkit-overflow-scrolling: touch;
  position: absolute;
  right: 0;
  top: calc(100% + 0.5em);
  width: 80vw;
  max-width: 30em;
  box-shadow: 0 0 5px 0;
  padding: 0.7em 1em 0.4em;
  background: white;
  border-radius: ${props => props.theme.smallBorderRadius};
  > * + * {
    padding-top: 1em !important;
    border-top: 2px solid ${props => props.theme.darkGray};
  }
  li + li {
    margin-top: 0.7em;
    padding-top: 0.7em;
    border-top: 1px solid ${props => props.theme.lightGray};
  }
  * {
    margin-top: 0;
    padding: 0;
  }
  ul {
    list-style: none;
  }
  mark {
    color: ${props => props.theme.lightBlue};
    background: ${props => props.theme.darkBlue};
  }
  header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.3em;
    h3 {
      color: white;
      background: ${props => props.theme.gray};
      padding: 0.1em 0.4em;
      border-radius: ${props => props.theme.smallBorderRadius};
    }
  }
  h3 {
    margin: 0 0 0.5em;
  }
  h4 {
    margin-bottom: 0.3em;
  }
`

export const PoweredBy = () => (
  <span css="font-size: 0.6em; text-align: end; padding: 0;">
    Powered by{` `}
    <a href="https://algolia.com">
      <Algolia size="1em" /> Algolia
    </a>
  </span>
)
```

Los estilos variarán de un sitio a otro, se muestran estos componentes solamente para tener la guía completa y además porque implementan comportamiento dinámico de la interfaz de búsqueda, me refiero al cuadro de texto que se desliza una vez que el usuario hace clic sobre el ícono `SearchIcon` (una lupa) y el panel que muestra los resultados de la búsqueda (`HitsWrapper`) que sólo aparece cuando los servidores de Algolia han retornado las coincidencias, dos funcionalidades que tal vez te interese conservar en tu código.

Ya casi hemos finalizado, solo faltan dos pequeños pasos. Primero necesitas construir un componente _hit_ para cada tipo de resultado que desees mostrar. En el ejemplo a continuación, encontrarás posts del blog y páginas. Y segundo, necesitas llamar a tu componente de búsqueda `Search` en algún lado de tu sitio. A continuación, puedes ver los componentes _hit_.

## `hitComps.js`

```js:title=src/components/search/hitComps.js
import React, { Fragment } from "react"
import { Highlight, Snippet } from "react-instantsearch-dom"
import { Link } from "gatsby"
import { Calendar } from "styled-icons/octicons/Calendar"
import { Tags } from "styled-icons/fa-solid/Tags"

export const PageHit = clickHandler => ({ hit }) => (
  <div>
    <Link to={hit.slug} onClick={clickHandler}>
      <h4>
        <Highlight attribute="title" hit={hit} tagName="mark" />
      </h4>
    </Link>
    <Snippet attribute="excerpt" hit={hit} tagName="mark" />
  </div>
)

export const PostHit = clickHandler => ({ hit }) => (
  <div>
    <Link to={`/blog` + hit.slug} onClick={clickHandler}>
      <h4>
        <Highlight attribute="title" hit={hit} tagName="mark" />
      </h4>
    </Link>
    <div>
      <Calendar size="1em" />
      &nbsp;
      <Highlight attribute="date" hit={hit} tagName="mark" />
      &emsp;
      <Tags size="1em" />
      &nbsp;
      {hit.tags.map((tag, index) => (
        <Fragment key={tag}>
          {index > 0 && `, `}
          {tag}
        </Fragment>
      ))}
    </div>
    <Snippet attribute="excerpt" hit={hit} tagName="mark" />
  </div>
)
```

`Highlight` y `Snippet` importados desde `react-instantsearch-dom` muestran al usuario atributos de resultados de coincidencias de búsquedas. Su diferencia es que el primero renderiza todo el texto (por ejemplo un título, fecha o etiqueta), mientras que el segundo solo muestra un fragmento del texto, es decir, un texto de un largo específico rodeando la cadena de coincidencia (para párrafos por ejemplo). En cada caso, el prop `attribute` deberá ser el nombre de la propiedad como fue asignada en `src/utils/algolia.js` y como aparece en tus índices del Algolia.

## Uso

Ahora, todo lo que se necesita es importar `Search` en algún lugar. El lugar obvio es el componente cabecera llamado `Header` así que, coloquémoslo ahí.

```js:title=src/components/Header/index.js
import React from "react"

import { Container, Logo } from "./styles"
import Nav from "../Nav"
import Search from "../Search"

const searchIndices = [
  { name: `Pages`, title: `Pages`, hitComp: `PageHit` },
  { name: `Posts`, title: `Blog Posts`, hitComp: `PostHit` },
]

const Header = ({ site, transparent }) => (
  <Container transparent={transparent}>
    <Logo to="/" title={site.title} rel="home" />
    <Nav />
    <Search collapse indices={searchIndices} />
  </Container>
)

export default Header
```

Nota que aquí es donde defines tu arreglo de índices de búsqueda y lo pasas como _prop_ a `Search`.

¡Si todo funciona como esperamos, al ejecutar `gatsby develop` deberías ver la magia de la búsqueda instantánea como se muestra en el video de abajo! Además puedes mirar y jugar con el buscador implementado [aquí](https://janosh.io/blog).

`youtube: Amsub4xJ3Jc`

## Recursos adicionales

Si tienes algún problema o si quieres aprender más acerca del uso de Algolia para búsquedas, puedes mirar este tutorial de Jason Lengstorf:

`youtube: VSkXyuXzwlc`

Además, también puedes encontrar historias de compañías que usan Gatsby + Algolia [en la sección del blog de Algolia](/blog/tags/algolia).
