---
title: SEO con Gatsby
---

<<<<<<< HEAD
Gatsby ayuda a mejorar la posición de tú sitio en los buscadores. Algunas funciones vienen listas y otras requieren configuración.
=======
Gatsby can help your site rank and perform better in search engines. Using Gatsby makes your site fast and efficient for search engine crawlers, like Googlebot, to crawl your site and index your pages. Some advantages, like speed, come out of the box and others require configuration.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Representación en el lado del servidor

<<<<<<< HEAD
Debido a que Gatsby es representado en el servidor, todo el contenido de la página queda disponible para Google y otros motores de busqueda o robots exploradores.

Tú puedes ver el código que ven los robots exploradores con `curl` (en tu terminal):
=======
Because Gatsby pages are server-side rendered, all the page content is available to Googlebot and other search engine crawlers.
You can see this by viewing the source for this page in your browser, Right-Click => View source. You'll see the fully rendered HTML document.

When you've installed [`gatsby-plugin-offline`](/packages/gatsby-plugin-offline/), you'll see a partial HTML document that does not contain the HTML you were hoping for. By using `gatsby-plugin-offline`, we can optimize bandwidth consumption and not let your users download too much data. Serving a partial HTML document is okay. Google and other search engines will still see the full HTML because `gatsby-plugin-offline` only starts working on the second-page load. A search engine always runs a page in Sandbox mode, which essentially is the first visit.

As a website owner, how do I test my site is serving its HTML correctly when `gatsby-plugin-offline` is being used? It would be best if you used your terminal of choice to visit your website. You can crawl your site by running the following command:

**on Windows (using powershell):**
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
Invoke-WebRequest https://www.gatsbyjs.org/docs/seo | Select -ExpandProperty Content
```

<<<<<<< HEAD
`Click-Derecho => Ver código fuente` no mostrará el HTML actual (pero la página sigue siendo procesada por el servidor!) porque este sitio usa workers. [Lee estas notas](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-offline#notes) para aprender más al respecto.
=======
**on Mac OS/Linux:**

```shell
curl https://www.gatsbyjs.org/docs/seo
```
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Aumento de velocidad

Gatsby incluye muchas herramientas para optimizar el rendimiento, tales como procesar archivos estáticos, carga de imágenes progresivas y el [modelo PRPL](/docs/prpl-pattern/)— todos ayudan a que tu sitio sea ligero y rápido por defecto.

<<<<<<< HEAD
Desde enero de 2018, Google [premia sitios más rápidos con un aumento en las clasificaciones de búsqueda](https://searchengineland.com/google-speed-update-page-speed-will-become-ranking-factor-mobile-search-289904).
=======
In July 2018, [Google announced a new ranking factor for site speed](https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html), calling the algorithm update the "Speed Update". Google will possibly rank pages higher in the search results for faster loading times, however, the intent of the search query is still very relevant and a slower page can rank higher if the content is more relevant.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Metadatos de la página

<<<<<<< HEAD
Agregando metadatos a la página, como título y descripción, ayuda a los buscadores a entender el contenido y cuando mostrar tu página en los resultados de busqueda.
=======
Adding metadata to pages, such as page title, meta description, alt text and structured data using JSON-LD, helps search engines understand your content and when to show your pages in search results.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

La forma común de agregar metadatos es agregar componentes de [react-helmet](https://github.com/nfl/react-helmet) (junto con [Gatsby React Helmet plugin](/packages/gatsby-plugin-react-helmet) para darle soporte al procesado en el servidor) a tu página. Aquí una guía de [como agregar componentes de SEO](https://www.gatsbyjs.org/docs/add-seo-component/) a tu aplicación de Gatsby.

Algunos ejemplos que usan react-helmet:

- [GatsbyJS.org sitio oficial](https://github.com/gatsbyjs/gatsby/blob/87ad6e81b9bd78b25d089434600750f5903baaee/www/src/components/package-readme.js#L16-L25)
- [GatsbyJS starter oficial por defecto](https://github.com/gatsbyjs/gatsby/blob/776dc1d6fe8d5ce7b5ea6d884736bb3c76280975/starters/default/src/components/seo.js)
- [Gatsby Correo](https://github.com/DSchau/gatsby-mail/blob/89b467e5654619ffe3073133ef0ae48b4d7502e3/src/components/meta.js)
- [Jason Lengstorf’s blog personal](https://github.com/jlengstorf/gatsby-theme-jason-blog/blob/e6d25ca927afdc75c759e611d4ba6ba086452bb8/src/components/SEO/SEO.js)

## Genera fragmentos enriquecidos en motores de búsqueda utilizando datos estructurados

<<<<<<< HEAD
Google utiliza datos estructurados que encuentra en la web para comprender el contenido de la página, así como para recopilar información sobre la web y el mundo en general.
Por ejemplo, aquí hay un fragmento de datos estructurados en el [formato JSON-LD](https://developers.google.com/search/docs/guides/intro-structured-data) (JavaScript Object Notation for Linked Data) que puede aparecer en la página de contacto de una empresa llamada Spooky Technologies, que describe su información de contacto:
=======
Google uses structured data that it finds on the web to understand the content of the page, as well as to gather information about the web and the world in general.

For example, here is a structured data snippet in the [JSON-LD format](https://developers.google.com/search/docs/guides/intro-structured-data) (JavaScript Object Notation for Linked Data) that might appear on the contact page of a company called Spooky Technologies, describing their contact information:
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```html
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Organization",
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

<<<<<<< HEAD
Cuando utilice datos estructurados, deberá realizar pruebas durante el desarrollo con la herramienta [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool) de Google es un método recomendado. Después del despliegue, su [Informe de estado enriquecidos](https://support.google.com/webmasters/answer/7552505?hl=en) puede ayudar a controlar el estado de tus páginas y mitigar cualquier problema de plantillas o publicación.
=======
When using structured data, you'll need to test during development and the [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool) from Google is one recommended method.

After deployment, their [Rich result status reports](https://support.google.com/webmasters/answer/7552505?hl=en) may help to monitor the health of your pages and mitigate any templating or serving issues.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Recursos adicionales

Tú también puedes estar interesado en el [articulo acerca del SEO en Gatsby](/blog/tags/seo/)
