---
title: "Añadiendo búsquedas"
overview: true
---

Mira abajo para ver una lista de guías en esta sección, o sigue leyendo un resumen sobre añadir la funcionalidad de búsquedas en tu sitio web.

<GuideList slug={props.slug} />

## Resumen de búsqueda en sitio web

Antes que vayamos a través de los pasos para añadir búsquedas a tu sitio web Gatsby, examinemos los componentes necesarios para añadir búsquedas a una página web.

Hay tres componentes requeridos para añadir búsquedas a tu página Gatsby:

1.  índice
2.  motor
3.  UI

## Componentes de búsquedas

### índice de búsquedas

El índice de búsquedas es una copia de tus datos almacenados en un formato amigable para búsquedas. El índice se utiliza para optimizar la búsqueda y el rendimiento cuando se ejecuta una petición de búsqueda. Sin un índice, cada búsqueda necesitaría escanear cada página en tu sitio web-lo que pronto se vuelve ineficiente.

### Motor de búsquedas

El motor de búsquedas recibe una petición de búsqueda, la ejecuta a través de los datos indexados y retorna cualquier documento coincidente.

### UI de búsquedas

El componente UI provee una interfaz al usuario, el cual le permite escribir peticiones de búsqueda y visualizar los resutados de cada petición.

## Añadiendo búsquedas a tu sitio web

Ahora que conoces los tres componentes requeridos, hay algunas formas de añadir búsquedas a tu sitio Gatsby.

### Usa un motor de búsquedas de código abierto

Usar un motor de búsquedas de código abierto es siempre gratuíto y te permite habilitar las búsquedas sin conexión en tu sitio web. Ten en cuenta que necesitas tener cuidado con las búsquedas sin conexión porque el índice completo ha de ser llevado al cliente, que puede afectar el tamaño del paquete significativamente.

Las librerías de código abierto como [`elasticlunr`](https://www.npmjs.com/package/elasticlunr) o [`js-search`](https://github.com/bvaughn/js-search) pueden ser usadas para habilitar las búsquedas en tu sitio web.

Para hacer eso necesitarás crear un índice de búsquedas cuando tu sitio web se construye. Para [`elasticlunr`](https://www.npmjs.com/package/elasticlunr), hay un plugin llamado [`gatsby-plugin-elasticlunr-search`](https://github.com/gatsby-contrib/gatsby-plugin-elasticlunr-search) que crea el indexado de búsquedas automáticamente.

Para otras librerías, puedes usar una combinación de [`onCreateNode`](/docs/node-apis/#onCreateNode), [`setFieldsOnGraphQLNodeType`](/docs/node-apis/#setFieldsOnGraphQLNodeType) y [`sourceNodes`](/docs/node-apis/#sourceNodes) de la API node de Gatsby para crear el indexado de búsqueda y hacerlo disponible en GraphQL. Para más información de cómo hacerlo echa un vistazo al [código fuente de `gatsby-plugin-elasticlunr-search`](https://github.com/gatsby-contrib/gatsby-plugin-elasticlunr-search/blob/master/src/gatsby-node.js#L96-L131).

Otra opción es generar el índice al finalizar la construcción usando la API node [`onPostBuild`](/docs/node-apis/#onPostBuild). Esta aproximación la usa [`gatsby-plugin-lunr`](https://github.com/humanseelabs/gatsby-plugin-lunr) para crear un índice multilenguaje.

Tras construir el índice de búsquedas e incluirlo en la capa de datos de Gatsby, necesitarás permitir al usuario buscar en tu sitio. Esto se hace habitualmente usando una entrada de texto para capturar la petición de búsqueda, y tras eso usar una de las librerías mencionadas arriba para obtener el/los documento(s) deseado(s)

### Usar un motor de búsquedas basado en API

Otra opción es usar un motor de búsquedas externo. Esta solución es mucho más escalable ya que los visitantes a tu sitio no tienen que descargar tu índice de búsquedas entero (que se vuelve muy pesado mientras tu sitio web crece) para buscar en tu sitio. La contrapartida es que necesitarás pagar por el alojamiento del motor de búsquedas o pagar por un servicio comercial de búsquedas.

Hay muchos disponibles de código abierto que puedes alojar tu mismo y opciones de alojamiento comercial.

- [ElasticSearch](https://www.elastic.co/products/elasticsearch) — Código abierto y con alojamiento comercial disponible
- [Solr](http://lucene.apache.org/solr/) — Código abierto y con alojamiento comercial disponible
- [Algolia](https://www.algolia.com/) — Comercial

Si estás creando una página de documentación, puede usar la [búsqueda de documentos de Algolia](https://community.algolia.com/docsearch/). Creará automáticamente un índice de búsquedas del contenido de tus páginas.

Si tu página web no se considera documentación, necesitarás rellenar el índice de búsquedas en tiempo de construcción y subirlo usando [`gatsby-plugin-algolia`](https://github.com/algolia/gatsby-plugin-algolia).

Cuando uses Algolia, ellos alojan el índice de búsquedas y el motor por ti. Tus peticiones serán enviadas a sus servidores, que responderán si hay resultados. Necesitarás implementar tu propia UI (interfaz de usuario); Algolia provee una [librería React](https://github.com/algolia/react-instantsearch) que podría tener componentes que podrías usar.

Elasticsearch tiene varias librerías de componentes React para búsquedas, p.ej. https://github.com/appbaseio/reactivesearch
