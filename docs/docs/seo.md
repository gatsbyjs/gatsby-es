---
title: SEO con Gatsby
---

Gatsby ayuda a mejorar la posición de tú sitio en los buscadores. Algunas funciones vienen listas y otras requieren configuración.

## Representación en el lado del servidor

Debido a que Gatsby es representado en el servidor, todo el contenido de la página queda disponible para Google y otros motores de busqueda o robots exploradores.

Tú puedes ver el código que ven los robots exploradores con `curl` (en tu terminal):

```shell
curl https://www.gatsbyjs.org/docs/seo
```

`Click-Derecho => Ver código fuente` no mostrará el HTML actual (pero la página sigue siendo procesada por el servidor!) porque este sitio usa workers. [Lee estas notas](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-offline#notes) para aprender más al respecto.

## Aumento de velocidad

Gatsby incluye muchas herramientas para optimizar el rendimiento, tales como procesar archivos estáticos, carga de imágenes progresivas y el [modelo PRPL](/docs/prpl-pattern/)— todos ayudan a que tu sitio sea ligero y rápido por defecto.

Desde enero de 2018, Google [premia sitios más rápidos con un aumento en las clasificaciones de búsqueda](https://searchengineland.com/google-speed-update-page-speed-will-become-ranking-factor-mobile-search-289904).

## Metadatos de la página

Agregando metadatos a la página, como título y descripción, ayuda a los buscadores a entender el contenido y cuando mostrar tu página en los resultados de busqueda.

La forma común de agregar metadatos es agregar componentes de [react-helmet](https://github.com/nfl/react-helmet) (junto con [Gatsby React Helmet plugin](/packages/gatsby-plugin-react-helmet) para darle soporte al procesado en el servidor) a tu página. Aquí una guía de [como agregar componentes de SEO](https://www.gatsbyjs.org/docs/add-seo-component/) a tu aplicación de Gatsby.

Algunos ejemplos que usan react-helmet:

- [GatsbyJS.org sitio oficial](https://github.com/gatsbyjs/gatsby/blob/87ad6e81b9bd78b25d089434600750f5903baaee/www/src/components/package-readme.js#L16-L25)
- [GatsbyJS starter oficial por defecto](https://github.com/gatsbyjs/gatsby/blob/776dc1d6fe8d5ce7b5ea6d884736bb3c76280975/starters/default/src/components/seo.js)
- [Gatsby Correo](https://github.com/DSchau/gatsby-mail/blob/89b467e5654619ffe3073133ef0ae48b4d7502e3/src/components/meta.js)
- [Jason Lengstorf’s blog personal](https://github.com/jlengstorf/gatsby-theme-jason-blog/blob/e6d25ca927afdc75c759e611d4ba6ba086452bb8/src/components/SEO/SEO.js)

## Genera fragmentos enriquecidos en motores de búsqueda utilizando datos estructurados

Google utiliza datos estructurados que encuentra en la web para comprender el contenido de la página, así como para recopilar información sobre la web y el mundo en general.
Por ejemplo, aquí hay un fragmento de datos estructurados en el [formato JSON-LD](https://developers.google.com/search/docs/guides/intro-structured-data) (JavaScript Object Notation for Linked Data) que puede aparecer en la página de contacto de una empresa llamada Spooky Technologies, que describe su información de contacto:

```js
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Company",
  "url": "http://www.spookytech.com",
  "name": "Spooky technologies",
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+5-601-785-8543",
    "contactType": "Customer Support"
  }
}
</script>
```

Cuando utilice datos estructurados, deberá realizar pruebas durante el desarrollo con la herramienta [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool) de Google es un método recomendado. Después del despliegue, su [Informe de estado enriquecidos](https://support.google.com/webmasters/answer/7552505?hl=en) puede ayudar a controlar el estado de tus páginas y mitigar cualquier problema de plantillas o publicación.

## Recursos adicionales

Tú también puedes estar interesado en el [articulo acerca del SEO en Gatsby](/blog/tags/seo/)
