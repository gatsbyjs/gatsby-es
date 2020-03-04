---
title: Creando un _Starter_
---

[_Los starters_](/docs/starters/) son proyectos tipo plantilla que los desarrolladores Gatsby pueden usar para configurar un nuevo sitio rápidamente. Antes de crear un _starter_, puede ser útil examinar detenidamente la [Librería de _Starters_ de Gatsby](/starters/) para ver lo que ya existe y determinar cómo tu _starter_ puede aportar valor.

## Requerimientos básicos

Para que un _starter_ funcione adecuadamente, necesita incluir algunos ficheros (mira el [_starter_ Hola Mundo](https://github.com/gatsbyjs/gatsby-starter-hello-world/) para ver un ejemplo del tipo esqueleto):

- `README.md`: instrucciones de cómo instalar y configurar tu _starter_, una lista de sus características o estructura, y cualquier consejo útil.
- `package.json`: el "centro de control" para las dependencias y _scripts_ de Gatsby. Encuentra un ejemplo en el archivo [package.json del _starter_ Hola Mundo](https://github.com/gatsbyjs/gatsby-starter-hello-world/blob/master/package.json).
- `gatsby-config.js`: un espacio para agregar datos configurables y _plugins_. Mira la [Configuración de Gatsby](/docs/gatsby-config/) para más información.
- `src/pages`: un directorio donde viven los componentes de página, con al menos un [archivo index.js (ejemplo)](https://github.com/gatsbyjs/gatsby-starter-hello-world/blob/master/src/pages/index.js).
- `static`: un directorio para archivos estáticos, como un archivo `favicon.ico`.
- `.gitignore`: un archivo que le dice a Git qué recursos dejar fuera del control de versiones, como el directorio `node_modules`, archivos de registro, el `.cache` de Gatsby y el directorio `public`.
- `.prettierrc` _(opcional)_: un archivo de configuración para [Prettier](https://prettier.io/), un _linter_ JavaScript y formateador usado para desarrollar en Gatsby.

Tu _starter_ también debería tener estas cualidades:

- Código abierto y disponible desde una URL estable
- Configurable
- Rápido
- Accesibilidad web

Explicamos sobre estos elementos para prepararte para crear un _starter_ ganador.

## Código abierto y disponible desde una URL estable

La CLI de Gatsby permite a los usuarios instalar un nuevo sitio con un _starter_ usando el comando `gatsby new <nombre-del-sitio> <url-del-starter>`. Para que esto funcione, tu _starter_ necesita estar disponible para descargar. La forma más fácil para conseguir esto es alojar tu _starter_ en GitHub o GitLab y usar la URL del repositorio disponible públicamente, como:

`gatsby new mi-aplicacion https://github.com/gatsbyjs/gatsby-starter-blog`

Aunque los _starters_ oficiales están en el repositorio de Gatsby, miembros de la comunidad pueden ofrecer sus propios _starters_ desde sus propios repositorios. Aquí hay un ejemplo de instalación de un _starter_ de la comunidad:

`gatsby new mi-aplicacion https://github.com/netlify-templates/gatsby-starter-netlify-cms`

## Configurable

Los _starters_ deben utilizar metadatos en `gatsby-config.js` cuando sea posible, ya que este suele ser el primer sitio donde los usuarios buscarán información para configurar el sitio. Algunos ejemplos de cosas que podrías hacer configurables en el `gatsby-config` son:

- El título del sitio
- El nombre del autor, información de contacto, y biografía
- Los enlaces a redes sociales

Alternativamente, para _starters_ que se conectan a un _headless CMS_, los elementos específicos de un autor se pueden extraer en el _starter_ desde una plataforma CMS usando un _plugin_ fuente y GraphQL en su lugar. ¡Mostrar a los usuarios cómo se hace esto puede hacer que tu _starter_ sea muy útil!

También sería muy apreciado si se usan capacidades de temas incorporados y un archivo "tema" se proporciona para configurarlo, por ejemplo cuando se use _styled-components_ o un sistema de diseño.

## Rápido

Gatsby es bastante rápido por defecto. Para crear un _starter_ que soporte a los usuarios en la "forma Gatsby", querrás configurar una implementación de pruebas con tu _starter_ para depurar el rendimiento. Usando herramientas como [Lighthouse](https://developers.google.com/web/tools/lighthouse/) y [Webpagetest.org](https://www.webpagetest.org/), puedes evaluar la velocidad de tu sitio de pruebas y hacer cualquier mejora necesaria al código fuente del _starter_  para que tus usuarios se beneficien de la velocidad por defecto.

Si hay áreas del _starter_ que podrían verse afectadas por el usuario, puede ayudar añadir alguna documentación o comentarios en el código que le recuerden optimizar para rendimiento (p.ej. comprimir imágenes)

## Accesibilidad web

Además del rendimiento, crear un _starter_ libre de problemas de accesibilidad es una maravillosa manera de contribuir al ecosistema de Gatsby. Aquí hay algunos consejos para crear un _starter_ inclusivo y accesible:

- Uso adecuado del [contraste en el color](https://webaim.org/articles/contrast/). (¡Este es el problema de accesibilidad más común en la web!)
- Conservar [indicadores visuales del enfoque del teclado](https://webaim.org/techniques/keyboard/).
- Usar [textos alternativos en las imágenes](https://webaim.org/techniques/alttext/) en tus ejemplos.
- Recomienda y usa [HTML semántico](https://webaim.org/techniques/semanticstructure/) donde sea posible.
- [Añade _labels_ a los _inputs_ de tu formulario](https://webaim.org/techniques/forms/).

Para más ayuda sobre accesibilidad, consulta la [lista de verificación del Proyecto A11y](https://a11yproject.com/checklist) y [WebAIM](https://webaim.org). También puedes consultar los [consejos para crear aplicaciones web accesibles](https://www.deque.com/blog/accessibility-tips-in-single-page-applications/) con mucho JavaScript en el lado del cliente.

## Ejecutar un _starter_ localmente

Ya que los _starters_ son proyectos de Gatsby, puedes ejecutar `gatsby develop` o `gatsby build` y entonces `gatsby serve` para asegurarte de que el _starter_ está funcionando. Sí quieres estar extra seguro y asegurarte de que el comando `gatsby new`  funciona con tu _starter_, puedes ejecutar `gatsby new nombre-del-proyecto ../ruta/relativa/a/tu/starter`, reemplazando la parte final del comando con la ruta relativa apropiada.

## Añade tu _starter_ a la Librería de _Starters_ de Gatsby

Para asegurarte de que tu _starter_ es fácilmente localizable, eres bienvenido (pero no requerido) a añadirlo a la [Librería de _Starters_ de Gatsby](/contributing/submit-to-starter-library/). Añade etiquetas a tu _starter_ comprobando primero las existentes (como `contentful`, `csv`, etc.), ¡y añade más si es necesiario!

## Otras lecturas:

- [Cómo crear un _Starter_ en Gatsby](https://medium.com/@emasuriano/how-to-create-a-gatsby-starter-e7d53083a880) por Emanuel Suriano
- [Introducción a los temas de Gatsby](/blog/2018-11-11-introducing-gatsby-themes/) (ncluye información sobre los _starters_)
