---
title: Temas Referencia de la API
---

## Core Gatsby APIs

Los temas son sitios empaquetados de Gatsby que se envían como _plugins_, por lo que tienes acceso a todas las API's de Gatsby para modificar la configuración y funcionalidad predeterminadas.

- [Configuración Gatsby](https://www.gatsbyjs.org/docs/gatsby-config/)
- [Acciones](https://www.gatsbyjs.org/docs/actions/)
- [Interfaz Node](https://www.gatsbyjs.org/docs/node-interface/)
- ... [y más](https://www.gatsbyjs.org/docs/api-specification/)

Si eres nuevo en Gatsby puedes empezar siguiendo las guías para construir un sitio. Convertirlo en un tema más adelante será sencillo ya que los temas son sitios de Gatsby preempaquetados.

## Configuración

Los _plugins_ ahora pueden incluir un `gatsby-config` además de los demás archivos `gatsby-*`. Típicamente nos referimos a los _plugins_ que incluyen `gatsby-config.js` como un tema (más sobre esto en [composición de tema](#theme-composition)). Un típico `gatsby-config.js` en el sitio de un usuario que usa su tema podría verse así. En este ejemplo, pasamos dos opciones a `gatsby-theme-name`: `postsPath` y `colors`.

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-theme-name",
      options: {
        postsPath: "/blog",
        colors: {
          primary: "tomato"
        }
      }
    }
  ]
};
```

Ahora puedes acceder a opciones que son pasadas a tu tema en tu `gatsby-config`. Puedes utilizar las opciones para configurar el abastecimiento del sistema de archivos, aceptar diferentes elementos del menú de navegación, cambiar los colores por defecto de la marca y cualquier otra cosa que deseé configurar.

Para aprovechar las opciones que se pasan al configurar su tema en el sitio de un usuario, devuelve una función en el `gatsby-config.js` de tu tema. El argumento que recibe la función son las opciones que el usuario pasó.

```js:title=gatsby-config.js
module.exports = themeOptions => {
  console.log(themeOptions);
  // logs `postsPath` and `colors`

  return {
    plugins: [
      // ...
    ]
  };
};
```

Mientras se use la exportación de objetos habitual (`module.exports = {}`) en tu tema significa que puedes ejecutar el tema de forma independiente como su propio sitio, al usar una función en su tema para aceptar opciones deberás ejecutar el tema como parte de un sitio de ejemplo. Vea cómo el [iniciador de creación de temas] (https://github.com/gatsbyjs/gatsby/tree/master/themes/gatsby-starter-theme-workspace) lo maneja utilizando _Yarn Workspaces_.

### Accediendo a las opciones en otro lugar

Ten en cuenta que debido a que los temas son _plugins_, también puedes acceder a las opciones en cualquiera de los métodos de ciclo de vida a los que estás acostumbrado. Por ejemplo, en tu tema `gatsby-node.js`, puedes acceder a las opciones como segundo argumento para `createPages`:

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }, themeOptions) => {
  console.log(themeOptions);
};
```

## _Shadowing_

Dado que los temas generalmente se implementan como paquetes npm que otras personas usan en sus sitios, necesitamos una forma de modificar ciertos archivos, como los componentes de React, sin realizar cambios al código fuente del tema. A esto se le llama _Shadowing_.

_Shadowing_ es una API basada en un sistema de archivos que nos permite reemplazar un archivo con otro en el momento de la compilación. Por ejemplo, si tuviéramos un tema con un componente `Encabezado` podríamos reemplazar ese `Encabezado` con el nuestro creando un nuevo archivo en nuestro sitio y colocándolo en la ubicación correcta para que el sombreado lo encuentre.

### Overriding

Echando un vistzo más de cerca a nuestro ejemplo del `Encabezado`, digamos que queremos un tema llamado `gatsby-theme-amazing`. Ese tema usa un componente `Encabezado` para mostrar la navegación y otros elementos. La ruta al componente desde la raíz del paquete npm es `gatsby-theme-amazing/src/components/header.js`.

Nos gustaría que el componente `Encabezado` haga algo diferente (tal vez cambiar colores, tal vez agregar elementos de navegación adicionales, realmente cualquier cosa que se te ocurra). Para hacer eso, creamos un archivo en nuestro sitio en `src/gatsby-theme-amazing/components/header.js`. Ahora podemos exportar cualquier componente _React_ que queramos de este archivo y Gatsby lo usará en lugar del componente del tema.

> 💡 Nota: tú puedes espejear componentes desde otros sitios usando el mismo método. Lee más sobre aplicaciones avanzadas en [sombreado latente](https://johno.com/latent-component-shadowing).

### Extendiendo

En la última sección hablamos sobre reemplazar completamente un componente con otro. ¿Qué sucede si queremos hacer un cambio más pequeño que no requiera copiar/pegar todo el componente del tema en el nuestro? Podemos aprovechar la capacidad de extender componentes.

Tomando el ejemplo anterior de `Encabezado`, cuando escribimos nuestro archivo de sombreado en `src/gatsby-theme-amazing/components/header.js`, podemos importar el componente original y reexportarlo como tal, agregando nuestro propio _prop_ sustituido en el componente.

```js
import Header from "gatsby-theme-amazing/src/components/header";

// these props are the same as the original component would get
export default props => <Header {...props} myProp="true" />;
```

Tomando este enfoque significa que cuando actualizamos nuestro tema más tarde, también podemos aprovechar todas las actualizaciones del componente `Encabezado` porque no lo hemos reemplazado por completo, solo lo hemos modificado.

### ¿Qué ruta debe usarse para sombrear un archivo?

Hasta que desarrollemos herramientas para soportar el manejo automático del sombreado, deberás ubicar manualmente las rutas en un tema y crear las rutas correctas de sombreado en tu sitio.

Afortunadamente, la forma de hacerlo es solo unos pocos pasos. Tome el directorio `src` del tema, muévelo al frente de la ruta, luego escribe un archivo en esa ubicación en tu sitio. Mirando hacia atrás en nuestro ejemplo de `Encabezado`, esta es la ruta al componente en nuestro tema:

```text
gatsby-theme-amazing/src/components/header.js
```

y aquí está la ruta donde lo sombreamos en nuestro sitio:

```text
<your-site>/src/gatsby-theme-amazing/components/header.js
```

El Sombreado sólo funciona en archivos importados en el directorio `src`. Esto se debe a que el sombreado se construye sobre _Webpack_, por lo que el gráfico del módulo debe incluir el archivo sombreado.

Dado que podemos usar varios temas en un sitio determinado, hay muchos lugares potenciales para sombrear un archivo determinado (uno para cada tema y otro para el sitio del usuario). En el caso de que varios temas intenten sombrear `gatsby-theme-amazing/src/components/header.js`, el último tema incluido en la matriz de los complementos ganará. El sitio en sí tiene la máxima prioridad en el sombreado.

## Composición del tema

Los temas de Gatsby se pueden componer horizontal y verticalmente. La composición vertical se refiere a la clásica relación "padre/hijo". Un tema hijo declara un tema padre en la matriz de complementos del tema hijo.

```js:title=gatsby-theme-child/gatsby-config.js
module.exports = {
  plugins: [`gatsby-theme-parent`]
};
```

La composición Horizontal es cuando dos temas son utilizados juntos, como `gatsby-theme-blog` y `gatsby-theme-notes`.

```js:title=my-site/gatsby-config.js
module.exports = {
  plugins: [`gatsby-theme-blog`, `gatsby-theme-notes`]
};
```

Los temas en su núcleo son un algoritmo que combina múltiples archivos `gatsby-config.js` en una sola configuración que tu sitio puede usar para construirlo. Para hacer eso necesitamos definir cómo combinar dos archivos `gatsby-config.js` juntos. Antes de que podamos hacer eso, necesitamos aplanar las relaciones padre/hijo en una sola matriz. Esto da como resultado el orden final cuando se considera qué archivo de sombreado usar si hay varios disponibles.

Nuestro primer ejemplo da como resultado un orden final de `['gatsby-theme-parent', 'gatsby-theme-child']` (los padres siempre van antes que sus hijos para que puedan anular la funcionalidad), mientras que nuestro segundo ejemplo da como resultado `['gatsby-theme-blog', 'gatsby-theme-notes']`.

Una vez que tenemos el orden final de los temas, los fusionamos usando una función de reducción. [Esta función de reducción](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/merge-gatsby-config.js) especifica la forma en que cada _key_ en `gatsby-config.js` se unirá. A menos que se especifique lo contrario a continuación, el último valor gana.

- `siteMetadata` y `mapping` ambos se funsionarán profundamente usando la función `merge` de _lodash_. Esto significa que un tema puede establecer valores predeterminados en `siteMetadata` y el sitio puede anularlos usando el objeto estándar `siteMetadata` en `gatsby-config.js`.
- `plugins` se normalizan para eliminar duplicados, luego se concatenan juntos.
