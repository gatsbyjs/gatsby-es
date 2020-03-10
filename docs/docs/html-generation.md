---
title: Generacion de páginas HTML
---

> Esta documentación no está actualizada con la última versión de Gatsby.
>
> Las áreas desactualizadas son:
>
> - reemplazar menciones de `data.json` con `page-data.json`
>
> Puedes ayudar haciendo un PR para [actualizar esta documentación](https://github.com/gatsbyjs/gatsby/issues/14228).

En la [sección previa](/docs/production-app/), vimos como Gatsby usa webpack para generar los empaquetados Javascript requeridos para hacerse cargo de la experiencia del usuario una vez que la primera página HTML ha terminado de cargar. Pero, ¿cómo se generan las páginas HTML originales?

El proceso a alto nivel es:

1. Crear una configuración de webpack para renderizado de lado de servidor Node.js (SSR)
1. Construye un `render-page.js` que toma la ruta de la página y renderiza su HTML
1. Por cada página en redux, llama `render-page.js`

## Webpack

Para el primer paso, usamos webpack para construir un empaquetado Node.js optimizado. El punto de entrada para esto es llamado `static-entry.js`

## static-entry.js

[static-entry.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/cache-dir/static-entry.js) exporta una función que toma la ruta y regresa el HTML renderizado. Esto es lo que hace para crear ese HTML:

1. [Solicitar página, json y _chunk_ de fuentes de datos webpack](/docs/html-generation/#1-require-page-json-and-webpack-chunk-data-sources)
2. [Crear contenedores HTML React](/docs/html-generation/#2-create-html-react-container)
3. [Cargar página y datos](/docs/html-generation/#3-load-page-and-data)
4. [Crear componente página](/docs/html-generation/#4-create-page-component)
5. [Agregar enlace de precarga y etiquetas script](/docs/html-generation/#5-add-preload-link-and-script-tags)
6. [Inyectar información de página a CDATA](/docs/html-generation/#6-inject-page-info-to-cdata)
7. [Renderizar el documento HTML final](/docs/html-generation/#7-render-final-html-document)

#### 1. Solicitar página, json y _chunk_ de fuentes de datos webpack

A fin de optimizar el resto de operaciones, necesitamos algunas fuentes de datos para trabajar. Estas son:

##### sync-requires.js

Exporta `components` que es un mapa de componentChunkName para requerir sentencias para la ubicación del componente en el disco. Mira [Escribir páginas](/docs/write-pages/#sync-requiresjs).

##### data.json

Contiene todas las páginas (con componentChunkName, jsonName y ruta) y el dataPaths que mapea jsonName a dataPath. Mira [Escribir páginas](/docs/write-pages/#datajson) para más.

##### webpack.stats.json

Contiene un mapeo de componentChunkName de los trozos de webpack que lo componen. Mira [División de código](/docs/how-code-splitting-works/#webpackstatsjson) para más.

##### chunk-map.json

Contiene un mapeo de componentChunkName a sus trozos centrales (no-compartidos). Mira [División de código](/docs/how-code-splitting-works/#chunk-mapjson) para más.

#### 2. Crear contenedores HTML React

Creamos un componente `html` React que eventualmente será renderizado a un archivo. Tendrá props por cada sección (ejemplo `head`, `preBodyComponents`, `postBodyComponents`). Esto es propiedad de [default-html.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/cache-dir/default-html.js).

#### 3. Cargar página y datos

La única entrada de `static-entry.js` es una ruta. Por lo tanto, debemos buscar en la página esa ruta para encontrar su `componentChunkName` y `jsonName`. Esto se logra simplemente buscando en el arreglo de páginas contenidas en `data.json`. Debemos entonces cargar sus datos buscando en `dataPaths`.

#### 4. Crear componente página

Ahora estamos listos para crear un componente React para la página (dentro del contenedor Html). Esto es manejado por [RouteHandler](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/cache-dir/static-entry.js#L123). Su renderizado creará un elemento desde el componente en `sync-requires.js`.

#### 5. Agregar enlace de precarga y etiquetas script

Esto es cubierto por la documentación de [división de código](/docs/how-code-splitting-works/#construct-link-and-script-tags-for-current-page). Esencialmente creamos un `<link rel="preload" href="component.js">` en el head del documento, seguido de `<script src="component.js">` al final del documento. Por cada componente y página JSON.

#### 6. Inyectar información de página a CDATA

[production-app.js](/docs/production-app/#first-load) necesita saber de la página que esta renderizando. La forma en que pasamos esta información es configurándola en CDATA durante la generación de HTML, ya que conocemos esa página hasta este punto. Entonces agregamos lo siguiente a la [parte superior del documento HTML](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/cache-dir/static-entry.js#L325):

```html
/*
<![
  CDATA[ */
    window.page={
      "path": "/blog/2.js",
      "componentChunkName": "component---src-blog-2-js",
      jsonName": "blog-2-995"
    };
    window.dataPath="621/path---blog-2-995-a74-dwfQIanOJGe2gi27a9CLKHjamc";
  */ ]
]>
*/
```

#### 7. Renderizar el documento HTML final

Finalmente, llamamos a [react-dom](https://reactjs.org/docs/react-dom.html) y renderiza nuestro componente Html de nivel superior en una cadena y lo devuelve.

## build-html.js

Hemos creado los medios para generar HTML para una página. Este empaquetado webpack es guardado en `public/render-page.js`. A continuación, necesitamos usarlo para generar el HTML para todas las páginas del sitio.

La página HTML no depende de otras páginas. Entonces podemos realizar este paso en paralelo. Usamos la librería [jest-worker](https://github.com/facebook/jest/tree/master/packages/jest-worker) para hacer esto mas fácil. Por defecto [html-renderer-queue.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/html-renderer-queue.js) crea un grupo de _workers_ igual al numero de núcleos físicos en tu maquina. Puedes configurar el número de grupos pasando una variable de entorno opcional, [`GATSBY_CPU_COUNT`](/docs/multi-core-builds). Luego divide las páginas en grupos y las envía a los _workers_, que ejecutan [worker.js](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/worker.js).

Los _workers_ simplemente iteran sobre cada página en su partición y llaman a `render-page.js` con la página. Luego guarda el html para la ruta de las páginas en `/public`.

Una vez que todos los workers hayan terminado, ¡hemos terminado!
