---
title: Creando un Plugin "Transformador"
---

Hay dos tipos de _plugins_ que funcionan dentro del sistema de datos de Gatsby, _plugins_ "fuente"
y "transformador".

- **Fuente** son _plugins_ que "obtienen" datos desde ubicaciones remotas o locales en lo que
  Gatsby llama [nodos](/docs/node-interface/).
- **Transformador** son _plugins_ que "transforman" datos proporcionados por los _plugins_ fuente en nuevos
  nodos y/o campos de nodo.

El propósito de este documento es:

1.  Definir qué es un _plugin_ transformador de Gatsby, y
2.  Examinar una reimplementación simplificada de un _plugin_ existente, para demostrar cómo crear un _plugin_ transformador.

## ¿Qué hacen los _plugins_ transformadores?

Los _plugins_ transformadores "transforman" datos de un tipo a otro tipo. Usarás a menudo ambos _plugins_ de origen y transformadores en tus sitios Gatsby.

Este acoplamiento flexible entre los datos de origen y los _plugins_ transformadores permiten a los desarrolladores de Gatsby ensamblar rápidamente _pipelines_ complejos de transformación de datos con poco trabajo.

## ¿Cómo creas un _plugin_ transformador?

Al igual que un _plugin_ fuente, un _plugin_ transformador es un paquete NPM normal. Tiene un archivo `package.json` con dependencias opcionales así como un archivo `gatsby-node.js` donde implementas las APIs Node.js de Gatsby.

`gatsby-transformer-yaml` en un plugin transformador que busca nuevos nodos con un formato de archivo _text/yaml_ (p.ej. un archivo .yaml) y crea nuevos nodo(s) hijo YAML convirtiendo el origen YAML en objetos JavaScript.

Como ejemplo, reconstruyamos parcialmente un `gatsby-transformer-yaml` simplificado directamente en un sitio de ejemplo. Digamos que tenemos un sitio Gatsby predeterminado que incluye un archivo `src/data/example.yml`:

```yaml:title=src/data/example.yml
- name: Jane Doe
  bio: Developer based in Somewhere, USA
- name: John Smith
  bio: Developer based in Maintown, USA
```

### Asegúrate de que los datos se obtienen

Primero, en `gatsby-config.js`, usa el plugin `gatsby-source-filesystem` para crear nodos _File_.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `./src/data/`,
      },
    },
  ],
}
```

Estos son expuestos en tu esquema _graphql_ que puedes consultar:

```graphql
query {
  allFile {
    edges {
      node {
        internal {
          type
          mediaType
          description
          owner
        }
      }
    }
  }
}
```

Ahora tienes un nodo `File` con el que trabajar:

```json
{
  "data": {
    "allFile": {
      "edges": [
        {
          "node": {
            "internal": {
              "contentDigest": "c1644b03f380bc5508456ce91faf0c08",
              "type": "File",
              "mediaType": "text/yaml",
              "description": "File \"src/data/example.yml\"",
              "owner": "gatsby-source-filesystem"
            }
          }
        }
      ]
    }
  }
}
```

### Transformar nodos de tipo `text/yaml`

Ahora, transforma los nuevos nodos `File` creados enganchándolos a la API `onCreateNode` en `gatsby-node.js`.

Si estás siguiendo en un proyecto de ejemplo, instala los siguientes paquetes:

```shell
npm install --save js-yaml lodash
```

Ahora, en `gatsby-node.js`:

```javascript:title=gatsby-node.js
const jsYaml = require(`js-yaml`)

async function onCreateNode({ node, loadNodeContent }) {
  // solo registra nodos con el mediaType `text/yaml`
  if (node.internal.mediaType !== `text/yaml`) {
    return
  }

  const content = await loadNodeContent(node)
  const parsedContent = jsYaml.load(content)
}

exports.onCreateNode = onCreateNode
```

Contenidos del archivo:

```text
- id: Jane Doe
  bio: Developer based in Somewhere, USA
- id: John Smith
  bio: Developer based in Maintown, USA
```

Contenido del archivo YAML resuelto:

```javascript
;[
  {
    id: "Jane Doe",
    bio: "Developer based in Somewhere, USA",
  },
  {
    id: "John Smith",
    bio: "Developer based in Maintown, USA",
  },
]
```

Ahora escribiremos una función auxiliar para transformar el contenido resuelto de YAML en nuevos nodos de Gatsby:

```javascript
function transformObject(obj, id, type) {
  const yamlNode = {
    ...obj,
    id,
    children: [],
    parent: node.id,
    internal: {
      contentDigest: createContentDigest(obj),
      type,
    },
  }
  createNode(yamlNode)
  createParentChildLink({ parent: node, child: yamlNode })
}
```

Arriba, creamos un objeto `yamlNode` con la forma esperada por la [acción `createNode`](/docs/actions/#createNode).

Luego creamos un enlace entre el nodo padre (archivo) y el nodo hijo (contenido yaml).

En nuestro `gatsby-node.js` actualizado, iteraremos a través del contenido resuelto en YAML, usando la función auxiliar para transformar cada uno en un nuevo nodo:

```javascript:title=gatsby-node.js
const jsYaml = require(`js-yaml`)
const _ = require(`lodash`)

async function onCreateNode({
  node,
  actions, // highlight-line
  loadNodeContent,
  createNodeId, // highlight-line
  createContentDigest, // highlight-line
}) {
  // highlight-start
  function transformObject(obj, id, type) {
    const yamlNode = {
      ...obj,
      id,
      children: [],
      parent: node.id,
      internal: {
        contentDigest: createContentDigest(obj),
        type,
      },
    }

    createNode(yamlNode)
    createParentChildLink({ parent: node, child: yamlNode })
  }
  // highlight-end

  const { createNode, createParentChildLink } = actions

  if (node.internal.mediaType !== `text/yaml`) {
    return
  }

  const content = await loadNodeContent(node)
  const parsedContent = jsYaml.load(content)

  // highlight-start
  parsedContent.forEach((obj, i) => {
    transformObject(
      obj,
      obj.id ? obj.id : createNodeId(`${node.id} [${i}] >>> YAML`),
      _.upperFirst(_.camelCase(`${node.name} Yaml`))
    )
  })
  // highlight-end
}

exports.onCreateNode = onCreateNode
```

Ahora podemos consultar nuestros nuevos nodos que contienen nuestros datos YAML transformados:

```graphql
query {
  allExampleYaml {
    edges {
      node {
        id
        name
        bio
      }
    }
  }
}
```

```json
{
  "data": {
    "allExampleYaml": {
      "edges": [
        {
          "node": {
            "id": "3baa5e64-ac2a-5234-ba35-7af86746713f",
            "name": "Jane Doe",
            "bio": "Developer based in Somewhere, USA"
          }
        },
        {
          "node": {
            "id": "2c733815-c342-5d85-aa3f-6795d0f25909",
            "name": "John Smith",
            "bio": "Developer based in Maintown, USA"
          }
        }
      ]
    }
  }
}
```

Revisa el [código fuente completo](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-transformer-yaml/src/gatsby-node.js) de `gatsby-transformer-yaml`.

## Usando la caché

A veces, transformar propiedades cuesta tiempo y recursos. Para evitar recrear estas propiedades en cada ejecución, puedes beneficiarte del mecanismo de caché global que proporciona Gatsby.

Las claves de caché deben contener al menos el contentDigest del nodo en cuestión. Por ejemplo, `gatsby-transformer-remark` usa la siguiente clave de caché para el nodo html:

```javascript:title=extend-node-type.js
const htmlCacheKey = node =>
  `transformer-remark-markdown-html-${node.internal.contentDigest}-${pluginsCacheStr}-${pathPrefixCacheStr}`
```

Acceder y configurar contenido en la caché es tan sencillo como:

```javascript:title=extend-node-type.js
const cachedHTML = await cache.get(htmlCacheKey(markdownNode))

cache.set(htmlCacheKey(markdownNode), html)
```
