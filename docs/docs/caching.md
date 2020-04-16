---
title: "Almacenando sitios estáticos en caché"
---

Una parte importante de crear un sitio web muy rápido es configurar correctamente el caché HTTP. El caché HTTP permite a los navegadores guardar en caché recursos de un sitio web, para que cuando el usuario vuelva al sitio, solo algunas partes del sitio necesiten ser descargadas.

Diferentes tipos de recursos son almacenados en caché de forma distinta. Veamos como los diferentes tipos de archivos compilados en `public/` deben ser guardados en caché.

## HTML

Los archivos HTML nunca deberían ser almacenados en caché por el navegador. Cuando se recompila el sitio Gatsby, generalmente se actualizan los contenidos de los archivos HTML. Por esto, los navegadores deben recibir la instrucción de controlar en cada petición si necesitan descargar una versión más nueva del archivo HTML.

La cabecera `cache-control` debe ser `cache-control: public, max-age=0, must-revalidate`<sup>1</sup>

## Datos de la página

Similar a los archivos HTML, los archivos JSON que se encuentran en el directorio `public/page-data/` no deberían ser guardados en caché por el navegador. De hecho, es posible actualizarlos sin la necesidad de volver a desplegar el sitio. Por esto, los navegadores deben recibir la instrucción de controlar en cada petición si los datos de la aplicación han cambiado.

La cabecera `cache-control` debe ser `cache-control: public, max-age=0, must-revalidate`<sup>1</sup>

## Archivos estáticos

Todos los archivos en el directorio `static/` deben ser guardados en caché para siempre. Para los archivos en este directorio, Gatsby crea rutas que son enlazadas directamente al contenido del archivo. Por lo que si el contenido del archivo cambia, la ruta también lo hace. Estas rutas no se ven como rutas normales, por ejemplo: `reactnext-gatsby-performance.001-a3e9d70183ff294e097c4319d0f8cff6-0b1ba.png`. Dado que el mismo archivo va a corresponder siempre a la misma ruta, Gatsby puede guardarlo en caché siempre.

La cabecera `cache-control` debe ser `cache-control: public, max-age=31536000, immutable`

## JavaScript y CSS

Los archivos JavaScript y CSS _generados por webpack_ deben también ser almacenados en caché para siempre. Igual que los archivos estáticos, Gatsby crea nombres de archivos JS y CSS (¡como un hash!) basados en el contenido del archivo. Si el contenido del archivo cambia, el hash también lo hará, por lo tanto estos archivos _generados por webpack_ son seguros de guardar en memoria caché.

La cabecera `cache-control` debe ser `cache-control: public, max-age=31536000, immutable`

La única excepción a esto es el archivo `/sw.js`, el cual necesita ser revalidado en cada carga para controlar si una nueva versión del sitio está disponible. Este archivo es generado por `gatsby-plugin-offline` y otros plugins, para poder servir contenido offline. Su cabecera `cache-control` debe ser `cache-control: public, max-age=0, must-revalidate`<sup>1</sup>

## Configurando el almacenamiento caché en diferentes proveedores

Cómo configurar el almacenamiento en caché depende de como esté organizado tu sitio. Puedes crear plugins de Gatsby por proveedor para automatizar la creación de las cabeceras de caché.

Se han creado los siguientes plugins:

- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify/)
- [gatsby-plugin-s3](https://github.com/jariz/gatsby-plugin-s3)

Para desplegar con Now, seguir las instrucciones en la [documentación de Now](https://zeit.co/guides/deploying-gatsby-with-now#bonus:-cache-your-gatsby-assets).

---

<sup>
  1
</sup> Puedes usar 'no-cache' en lugar de 'max-age=0, must-revalidate'. A pesar de lo que el nombre pueda implicar, 'no-cache' permite al cache servir contenido en cache siempre y cuando se valide lo reciente del cache primero.
<sup>
  [2][3]{" "}
</sup> En cualquier caso, los clientes deben hacer un viaje de ida y vuelta al servidor de origen por cada solicitud. Sin embargo, si estas utilizando correctamente la validación de "ETags" o "Last-Modified" evitaras descargar recursos cuando la copia en cache siga siendo valida. (p. ej. el archivo no ha cambiado en el servidor de origen desde que fue puesto en cache).

[2]: https://tools.ietf.org/html/rfc7234#section-5.2.2.1
[3]: https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#no-cache_and_no-store
