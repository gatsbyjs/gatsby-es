---
title: Localización e internacionalización con Gatsby (i18n)
---

Servir contenido a los usuarios de una manera que se adapte a su idioma y cultura es parte de una excelente experiencia de usuario. Cuando haces un esfuerzo por adaptar el contenido web a la ubicación de un usuario, esa práctica se llama internacionalización (i18n).

En la práctica, i18n implica traducir texto y formatear fechas, números y cadenas según la ubicación detectada por el usuario. Por ejemplo, una fecha que se muestra para un usuario en los Estados Unidos seguiría el formato de fecha mm/dd/año, pero para un usuario en el Reino Unido el formato de fecha cambiaría a dd/mm/año.

Esta guía es un breve vistazo a las opciones que existen para mejorar tu proyecto Gatsby para la internacionalización.

## Elegir un paquete

Hay algunos paquetes React i18n por ahí. Varias opciones incluyen [react-intl](https://github.com/yahoo/react-intl), la comunidad [Gatsby plugin] (https://www.npmjs.com/package/gatsby-plugin-i18n) y [react-i18next] (https://github.com/i18next/react-i18next/). Hay varios factores a considerar al elegir un paquete: ¿Ya utilizas un paquete similar en otro proyecto? ¿Qué tan bien satisface las necesidades de tus usuarios este paquete? ¿Tu o tu equipo ya están familiarizados con cierto paquete? ¿El paquete está bien documentado y mantenido?

### gatsby-plugin-i18n

Este plugin te ayuda a usar `react-intl`, `i18next` o cualquier otra biblioteca i18n con Gatsby. Este complemento no traduce ni formatea tu contenido, sino que crea rutas para cada idioma, lo que permite a Google encontrar más fácilmente la versión correcta de tu sitio y, si es necesario, designar diseños de interfaz de usuario alternativos.

El formato de nombres sigue. **languageKey**. Js para archivos y /**languageKey**/ruta/NombreDelArchivo para URL.

**Ejemplo:**

Archivo - src/pages/about.**en**.js

URL - /**en**/about

[gatsby-plugin-i18n en GitHub](https://github.com/angeloocana/gatsby-plugin-i18n)

### react-intl

React-intl forma parte del conjunto de bibliotecas i18n de FormatJS y proporciona soporte para más de 150 idiomas. Se basa en la [Internacionalizacion API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl) que proporciona API y componentes mejorados. React-intl utiliza el contexto React y los HOC (componentes de orden superior) para proporcionar traducciones que le permiten cargar dinámicamente módulos de idioma a medida que los necesita. También hay opciones de polyfill disponibles para navegadores antiguos que no admiten la API base de JavaScript i18n.

Información más detallada sobre react-intl's [APIs](https://github.com/formatjs/react-intl/blob/master/docs/API.md) y [componentes](https://github.com/formatjs/react-intl/blob/master/docs/Components.md), incluyendo [demos](https://github.com/formatjs/react-intl/tree/master/examples), están disponibles en la [documentación] (https://github.com/formatjs/react-intl/tree/master/docs).

### react-i18next

React-i18next es una biblioteca de internacionalización construida en el framework i18next. Utiliza componentes para asegurarse de que las traducciones se procesen correctamente o para volver a representar tu contenido cuando cambie el idioma del usuario.

React-i18next es más extensible que otras opciones con una variedad de complementos, utilidades y configuraciones. Los complementos comunes permiten detectar el idioma de un usuario o agregar una capa adicional de almacenamiento en caché local. Otras opciones incluyen el almacenamiento en caché, un complemento de back-end para cargar traducciones de su servidor o agrupar traducciones con Webpack.

Este framework también tiene soporte experimental para la API React suspense y React Hooks.

## Otros recursos

- [Construyendo i18n con Gatsby](https://www.gatsbyjs.org/blog/2017-10-17-building-i18n-with-gatsby/)

- [Construyendo Eviction Free NYC con GatsbyJS + Contentful](https://www.gatsbyjs.org/blog/2018-04-27-building-eviction-free-nyc-with-gatsbyjs-and-contentful/)

- [Gatsby i18n paquetes](https://www.gatsbyjs.org/packages/gatsby-plugin-i18n/?=i18)

- [Gatsby i18n articulos](https://www.gatsbyjs.org/blog/tags/i-18-n/)
- [Recursos i18n de W3C](http://w3c.github.io/i18n-drafts/getting-started/contentdev.en#reference)
