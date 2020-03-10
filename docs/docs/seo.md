---
title: SEO con Gatsby
---

Gatsby ayuda a mejorar la posición de tú sitio en los buscadores. Usar Gatsby hace que tu sitio sea rápido y eficiente para los rastreadores (`crawlers`) de los motores de búsqueda, como Googlebot, para rastrear tu sitio e indexar tus páginas. Algunas ventajas, como velocidad, vienen listas de inmediato y otras requieren configuración.

## Representación en el lado del servidor

Debido a que Gatsby es renderizado en el servidor, todo el contenido de la página queda disponible para Google y otros motores de búsqueda o robots exploradores.
Puedes ver esto inspeccionando la fuente para está página en el navegador, Click-Derecho => Ver el código fuente de la página. Verás el documento HTML completo renderizado.

Cuando instalas [`gatsby-plugin-offline`](/packages/gatsby-plugin-offline/), verás un documento HTML parcial que no contiene el HTML que esperabas. Usando `gatsby-plugin-offline`, podemos optimizar el consumo de ancho de banda y no dejar que los usuarios descarguen demasiados datos. Sirviendo un documento HTML parcial está bien. Google y otros motores de búsqueda aún verán el HTML completo debido a que `gatsby-plugin-offline` solo empieza a funcionar en la segunda carga de la página. Un motor de búsqueda siempre sirve una página en modo `Sandbox`, que esencialmente es la primera visita.

Como dueño de un sitio web, ¿como puedo probar que mi sitio está sirviendo su HTML correctamente cuando `gatsby-plugin-offline` está siendo usado? Lo mejor sería si utilizarás una terminal de tu preferencia para visitar tu sitio. Puedes rastrear tu sitio ejecutando el siguiente comando:

**en Windows (utilizando powershell):**

```shell
Invoke-WebRequest https://www.gatsbyjs.org/docs/seo | Select -ExpandProperty Content
```

**en Mac OS/Linux:**

```shell
curl https://www.gatsbyjs.org/docs/seo
```

## Aumento de velocidad

Gatsby incluye muchas herramientas para optimizar el rendimiento, tales como procesar archivos estáticos, carga de imágenes progresivas y el [modelo PRPL](/docs/prpl-pattern/)— todos ayudan a que tu sitio sea ligero y rápido por defecto.

En Julio de 2018, [Google anunció un nuevo factor de posicionamiento para las velocidades de sitios](https://webmasters.googleblog.com/2018/01/using-page-speed-in-mobile-search.html), nombrando el algoritmo de actualización "Velocidad de Actualización". Google posiblemente posicionará páginas mejor en los resultados de búsqueda por mejores tiempos de carga, sin embargo, la intención de la búsqueda sigue siendo muy relevante y una página más lenta puede posicionarse mejor porque su contenido es más relevante.

## Metadatos de la página

Agregando metadatos a la página, como título, descripción, textos `alt` y datos estructurados usando JSON-LD ayuda a los buscadores a entender el contenido y cuando mostrar tu página en los resultados de busqueda.

La forma común de agregar metadatos es agregar componentes de [react-helmet](https://github.com/nfl/react-helmet) (junto con [Gatsby React Helmet plugin](/packages/gatsby-plugin-react-helmet) para darle soporte al procesado en el servidor) a tu página. Aquí una guía de [como agregar componentes de SEO](https://www.gatsbyjs.org/docs/add-seo-component/) a tu aplicación de Gatsby.

Algunos ejemplos que usan react-helmet:

- [GatsbyJS.org sitio oficial](https://github.com/gatsbyjs/gatsby/blob/87ad6e81b9bd78b25d089434600750f5903baaee/www/src/components/package-readme.js#L16-L25)
- [GatsbyJS starter oficial por defecto](https://github.com/gatsbyjs/gatsby/blob/776dc1d6fe8d5ce7b5ea6d884736bb3c76280975/starters/default/src/components/seo.js)
- [Gatsby Correo](https://github.com/DSchau/gatsby-mail/blob/89b467e5654619ffe3073133ef0ae48b4d7502e3/src/components/meta.js)
- [Jason Lengstorf’s blog personal](https://github.com/jlengstorf/gatsby-theme-jason-blog/blob/e6d25ca927afdc75c759e611d4ba6ba086452bb8/src/components/SEO/SEO.js)

## Genera fragmentos enriquecidos en motores de búsqueda utilizando datos estructurados

Google utiliza datos estructurados que encuentra en la web para comprender el contenido de la página, así como para recopilar información sobre la web y el mundo en general.

Por ejemplo, aquí hay un fragmento de datos estructurados en el [formato JSON-LD](https://developers.google.com/search/docs/guides/intro-structured-data) (JavaScript Object Notation for Linked Data) que puede aparecer en la página de contacto de una empresa llamada Spooky Technologies, que describe su información de contacto:

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

Cuando utilices datos estructurados, deberás realizar pruebas durante el desarrollo con la herramienta [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool) de Google es un método recomendado. 

Después del despliegue, tu [Informe de estado enriquecido](https://support.google.com/webmasters/answer/7552505?hl=es) puede ayudar a controlar el estado de tus páginas y mitigar cualquier problema de plantillas o publicación.

## Recursos adicionales

Tú también puedes estar interesado en el [articulo acerca del SEO en Gatsby](/blog/tags/seo/)
