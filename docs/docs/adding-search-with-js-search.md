---
title: Agregando búsquedas con js-search
---

## Prerrequisitos

Antes de realizar los pasos necesarios para agregar búsquedas en el lado-del-cliente de tu sitio web Gatsby, debes estar familiarizado con lo básico en Gatsby. Revisa el [tutorial](/tutorial/) y repasa la [documentación](/docs/) si lo necesitas. Adicionalmente, algún conocimiento de la [sintaxis ES6](https://medium.freecodecamp.org/write-less-do-more-with-javascript-es6-5fd4a8e50ee2) será de utilidad.

## Qué es JS Search

[JS Search](https://github.com/bvaughn/js-search) es una librería creada por Brian Vaughn, un miembro del equipo del núcleo de Facebook. Provee una manera eficiente de buscar datos en el cliente con JavaScript y objetos JSON. También sus opciones de personalización son extensas, revisa sus docs para más detalles.

Todo el código y documentación de esta librería esta [disponible en GitHub](https://github.com/bvaughn/js-search). Esta guía está basada en el ejemplo oficial de `js-search`, pero ha sido adaptado para que funcione con tu sitio Gatsby.

## Montaje

Empezarás creando un nuevo sitio Gatsby basado en la plantilla oficial _hello world_. Abre una terminal y ejecuta el siguiente comando:

```shell
gatsby new js-search-example https://github.com/gatsbyjs/gatsby-starter-default
```

Después que el proceso se haya completado, se necesitan algunos paquetes adicionales.

Cambia de directorio a la carpeta `js-search-example` y lanza el siguiente comando:

```shell
npm install --save js-search axios
```

O si usas Yarn:

```shell
yarn add js-search axios
```

**Nota**:

Para este ejemplo en particular, se usará [axios](https://github.com/axios/axios) para manejar todas las peticiones HTTP basadas-en-promesas.

## Selección de estrategia

En las siguientes secciones aprenderás dos propuestas para implementar `js-search` en tu sitio. La que elijas dependerá de el número de _items_ que quieras buscar. Para un conjunto de datos de pequeño a medio, la primera estrategia documentada debe funcionar bien.

Para un conjunto de datos mas grandes puedes usar el segundo enfoque, ya que la mayor parte del trabajo se realiza de antemano mediante el uso de la _API_ interna de Gatsby.

Las dos maneras son bastante generales, fueron implementadas usando las opciones predefinidas de la librería, para que se pueda experimentar sin entrar en los detalles de la librería.

Y finalmente, mientras atraviesas el código, ten en mente que no se adhiere a las mejoras practicas, es solo para fines ilustrativos, en un sitio real se habría implementado de diferente manera.

## JS-Search con un conjunto de datos de pequeño a medio

Comienza creando un archivo llamado `SearchContainer.js` en la carpeta `src/components/`, después agrega el siguiente código para iniciar:

```javascript
import React, { Component } from "react"
import Axios from "axios"
import * as JsSearch from "js-search"

class Search extends Component {
  state = {
    bookList: [],
    search: [],
    searchResults: [],
    isLoading: true,
    isError: false,
    searchQuery: "",
  }
  /**
   * Método de ciclo de vida de React para obtener datos
   */
  async componentDidMount() {
    Axios.get("https://bvaughn.github.io/js-search/books.json")
      .then(result => {
        const bookData = result.data
        this.setState({ bookList: bookData.books })
        this.rebuildIndex()
      })
      .catch(err => {
        this.setState({ isError: true })
        console.log("====================================")
        console.log(`Something bad happened while fetching the data\n${err}`)
        console.log("====================================")
      })
  }

  /**
   * reconstruye el índice general en base a las opciones
   */
  rebuildIndex = () => {
    const { bookList } = this.state
    const dataToSearch = new JsSearch.Search("isbn")
    /**
     *  define una estrategia de índice para los datos
     * más acerca de esto aquí https://github.com/bvaughn/js-search#configuring-the-index-strategy
     */
    dataToSearch.indexStrategy = new JsSearch.PrefixIndexStrategy()
    /**
     * define el sanitizante para la búsqueda
     * para prevenir que algunas palabras sean excluidas
     *
     */
    dataToSearch.sanitizer = new JsSearch.LowerCaseSanitizer()
    /**
     * define el índice de la búsqueda
     * lee más aquí https://github.com/bvaughn/js-search#configuring-the-search-index
     */
    dataToSearch.searchIndex = new JsSearch.TfIdfSearchIndex("isbn")

    dataToSearch.addIndex("title") // establece el atributo índice para los datos
    dataToSearch.addIndex("author") // establece el atributo índice para los datos

    dataToSearch.addDocuments(bookList) // agrega los datos a ser buscados
    this.setState({ search: dataToSearch, isLoading: false })
  }

  /**
   * maneja el input change y realiza una búsqueda con js-search
   * en la cual el resultado será agregado a el estado
   */
  searchData = e => {
    const { search } = this.state
    const queryResult = search.search(e.target.value)
    this.setState({ searchQuery: e.target.value, searchResults: queryResult })
  }
  handleSubmit = e => {
    e.preventDefault()
  }

  render() {
    const { bookList, searchResults, searchQuery } = this.state
    const queryResults = searchQuery === "" ? bookList : searchResults
    return (
      <div>
        <div style={{ margin: "0 auto" }}>
          <form onSubmit={this.handleSubmit}>
            <div style={{ margin: "0 auto" }}>
              <label htmlFor="Search" style={{ paddingRight: "10px" }}>
                Enter your search here
              </label>
              <input
                id="Search"
                value={searchQuery}
                onChange={this.searchData}
                placeholder="Enter your search here"
                style={{ margin: "0 auto", width: "400px" }}
              />
            </div>
          </form>
          <div>
            Number of items:
            {queryResults.length}
            <table
              style={{
                width: "100%",
                borderCollapse: "collapse",
                borderRadius: "4px",
                border: "1px solid #d3d3d3",
              }}
            >
              <thead style={{ border: "1px solid #808080" }}>
                <tr>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Book ISBN
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Book Title
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Book Author
                  </th>
                </tr>
              </thead>
              <tbody>
                {queryResults.map(item => {
                  return (
                    <tr key={`row_${item.isbn}`}>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.isbn}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.title}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.author}
                      </td>
                    </tr>
                  )
                })}
              </tbody>
            </table>
          </div>
        </div>
      </div>
    )
  }
}
export default Search
```

Descomponiendo el código en partes más pequeñas:

1. Cuando el componente es montado, el método de ciclo de vida `componentDidMount()` es disparado y los datos seran obtenidos.
2. Si no ocurren errores, los datos recibidos son agregados al estado y la función `rebuildIndex()` es invocada.
3. El motor de búsqueda es entonces creado y configurado con las opciones por defecto.
4. Los datos son indexados usando js-search.
5. Cuando el contenido del _input_ cambia, js-search inicia el proceso de búsqueda basado en el valor del `input` y regresa los resultados de la búsqueda si hay, los cuales son presentados al usuario mediante el elemento `table`.

### Uniendo todas las piezas

Para que funcione en tu sitio, solo necesitarás importar el componente recientemente creado a una página.
Como puedes observar [en el sitio de ejemplo](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/src/pages/index.js).

Ejecuta `gatsby develop` y si todo fue bien, abre tu navegador preferido e introduce la url `http://localhost:8000` - tendrás una búsqueda completamente funcional a tu dispocición.

## JS-Search con un conjunto de datos grande

Ahora intentemos otro enfoque, esta ocasión en vez de dejar que el componente haga todo el trabajo, es responsabilidad de Gatsby que haga eso y pase todos los datos a la página definida en la propiedad ruta, via [pageContext](/docs/behind-the-scenes-terminology/#pagecontext).

Para hace esto, algunos cambios son requeridos.

Inicia modificando el archivo `gatsby-node.js` agregando el siguiente código:

```javascript
const path = require("path")
const axios = require("axios")

exports.createPages = ({ actions }) => {
  const { createPage } = actions
  return new Promise((resolve, reject) => {
    axios
      .get("https://bvaughn.github.io/js-search/books.json")
      .then(result => {
        const { data } = result
        /**
         * crea una página dinámica con los datos recibidos
         * inyecta los datos en el objeto contex junto con algunas opciones
         * para configurar js-search
         */
        createPage({
          path: "/search",
          component: path.resolve(`./src/templates/ClientSearchTemplate.js`),
          context: {
            bookData: {
              allBooks: data.books,
              options: {
                indexStrategy: "Prefix match",
                searchSanitizer: "Lower Case",
                TitleIndex: true,
                AuthorIndex: true,
                SearchByTerm: true,
              },
            },
          },
        })
        resolve()
      })
      .catch(err => {
        console.log("====================================")
        console.log(`error creating Page:${err}`)
        console.log("====================================")
        reject(new Error(`error on page creation:\n${err}`))
      })
  })
}
```

Crea un archivo llamado `ClientSearchTemplate.js` en la carpeta `src/templates/`, después agrega el siguiente código para empezar:

```javascript
import React from "react"
import ClientSearch from "../components/ClientSearch"

const SearchTemplate = props => {
  const { pageContext } = props
  const { bookData } = pageContext
  const { allBooks, options } = bookData
  return (
    <div>
      <h1 style={{ marginTop: `3em`, textAlign: `center` }}>
        Search data using JS Search using Gatsby Api
      </h1>
      <div>
        <ClientSearch books={allBooks} engine={options} />
      </div>
    </div>
  )
}

export default SearchTemplate
```

Create a file named `ClientSearch.js` in the `src/components/` folder, then add the following code as a baseline:

```javascript
import React, { Component } from "react"
import * as JsSearch from "js-search"

class ClientSearch extends Component {
  state = {
    isLoading: true,
    searchResults: [],
    search: null,
    isError: false,
    indexByTitle: false,
    indexByAuthor: false,
    termFrequency: true,
    removeStopWords: false,
    searchQuery: "",
    selectedStrategy: "",
    selectedSanitizer: "",
  }
  /**
   * Método de ciclo de vida de React que inyectará los datos al estado.
   */
  static getDerivedStateFromProps(nextProps, prevState) {
    if (prevState.search === null) {
      const { engine } = nextProps
      return {
        indexByTitle: engine.TitleIndex,
        indexByAuthor: engine.AuthorIndex,
        termFrequency: engine.SearchByTerm,
        selectedSanitizer: engine.searchSanitizer,
        selectedStrategy: engine.indexStrategy,
      }
    }
    return null
  }
  async componentDidMount() {
    this.rebuildIndex()
  }

  /**
   * reconstruye el índice general en base a las opciones
   */
  rebuildIndex = () => {
    const {
      selectedStrategy,
      selectedSanitizer,
      removeStopWords,
      termFrequency,
      indexByTitle,
      indexByAuthor,
    } = this.state
    const { books } = this.props

    const dataToSearch = new JsSearch.Search("isbn")

    if (removeStopWords) {
      dataToSearch.tokenizer = new JsSearch.StopWordsTokenizer(
        dataToSearch.tokenizer
      )
    }
    /**
     * define una estrategia de indexado para los datos
     * leé mas acerca de esto aquí https://github.com/bvaughn/js-search#configuring-the-index-strategy
     */
    if (selectedStrategy === "All") {
      dataToSearch.indexStrategy = new JsSearch.AllSubstringsIndexStrategy()
    }
    if (selectedStrategy === "Exact match") {
      dataToSearch.indexStrategy = new JsSearch.ExactWordIndexStrategy()
    }
    if (selectedStrategy === "Prefix match") {
      dataToSearch.indexStrategy = new JsSearch.PrefixIndexStrategy()
    }

    /**
     * define el sanitizante para la búsqueda
     * para prevenir que algunas palabras sean excluidas
     */
    selectedSanitizer === "Case Sensitive"
      ? (dataToSearch.sanitizer = new JsSearch.CaseSensitiveSanitizer())
      : (dataToSearch.sanitizer = new JsSearch.LowerCaseSanitizer())
    termFrequency === true
      ? (dataToSearch.searchIndex = new JsSearch.TfIdfSearchIndex("isbn"))
      : (dataToSearch.searchIndex = new JsSearch.UnorderedSearchIndex())

    // establece el atributo índice para los datos
    if (indexByTitle) {
      dataToSearch.addIndex("title")
    }
    // establece el atributo índice para los datos
    if (indexByAuthor) {
      dataToSearch.addIndex("author")
    }

    dataToSearch.addDocuments(books) // agrega los datos a ser buscados

    this.setState({ search: dataToSearch, isLoading: false })
  }
  /**
   * maneja los cambios en el input y realiza una búsqueda con js-search
   * en la cual el resultado será agregado a el estado
   */
  searchData = e => {
    const { search } = this.state
    const queryResult = search.search(e.target.value)
    this.setState({ searchQuery: e.target.value, searchResults: queryResult })
  }
  handleSubmit = e => {
    e.preventDefault()
  }
  render() {
    const { searchResults, searchQuery } = this.state
    const { books } = this.props
    const queryResults = searchQuery === "" ? books : searchResults
    return (
      <div>
        <div style={{ margin: "0 auto" }}>
          <form onSubmit={this.handleSubmit}>
            <div style={{ margin: "0 auto" }}>
              <label htmlFor="Search" style={{ paddingRight: "10px" }}>
                Enter your search here
              </label>
              <input
                id="Search"
                value={searchQuery}
                onChange={this.searchData}
                placeholder="Enter your search here"
                style={{ margin: "0 auto", width: "400px" }}
              />
            </div>
          </form>
          <div>
            Number of items:
            {queryResults.length}
            <table
              style={{
                width: "100%",
                borderCollapse: "collapse",
                borderRadius: "4px",
                border: "1px solid #d3d3d3",
              }}
            >
              <thead style={{ border: "1px solid #808080" }}>
                <tr>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Book ISBN
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Book Title
                  </th>
                  <th
                    style={{
                      textAlign: "left",
                      padding: "5px",
                      fontSize: "14px",
                      fontWeight: 600,
                      borderBottom: "2px solid #d3d3d3",
                      cursor: "pointer",
                    }}
                  >
                    Book Author
                  </th>
                </tr>
              </thead>
              <tbody>
                {queryResults.map(item => {
                  return (
                    <tr key={`row_${item.isbn}`}>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.isbn}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.title}
                      </td>
                      <td
                        style={{
                          fontSize: "14px",
                          border: "1px solid #d3d3d3",
                        }}
                      >
                        {item.author}
                      </td>
                    </tr>
                  )
                })}
              </tbody>
            </table>
          </div>
        </div>
      </div>
    )
  }
}
export default ClientSearch
```

Descomponiendo el código en partes más pequeñas:

1. Cuando el componente es montado, el método de ciclo de vida `getDerivedStateFromProps()` es invocado y evaluará el estado y si es necesario lo actualizará.
2. Despues el método de ciclo de vida `componentDidMount()` será disparado y la función `rebuildIndex()` es invocada.
3. El motor de búsqueda es entonces creado y configurado con las opciones definidas.
4. Los datos son indexados usando js-search.
5. Cuando el contenido del _input_ cambia, js-search inicia el proceso de búsqueda basado en el valor del `input` y regresa los resultados de la búsqueda si hay, los cuales son presentados al usuario mediante el elemento `table`.

### Uniendo todas las piezas

Nuevamente, para que funcione en tu sitio solo necesitas copiar [el archivo `gatsby-node.js` localizado aquí](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/gatsby-node.js).

Y tanto la [plantilla](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/src/templates/ClientSearchTemplate.js) como el [componente buscar](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-js-search/src/components/ClientSearch.js).

Lanzando `gatsby develop` nuevamente, y si todo salió sin detalles una vez más, abre tu navegador preferido e introduce la url `http://localhost:8000/search`, tendrás una búsqueda completamente funcional a tu dispocición acoplada con la API Gatsby.

Esperemos que esta guía bastante extensa haya arrojado algunas ideas sobre cómo implementar la búsqueda usando js-search en el lado del cliente.

¡Ahora ve y crea algo genial!