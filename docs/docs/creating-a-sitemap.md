---
title: Creando un Sitemap (Mapa del Sitio)
---

## ¿Qué es un sitemap?

Un [sitemap en XML](https://support.google.com/webmasters/answer/156184?hl=es) o también llamado "mapa del sitio" lista páginas importantes de un sitio web, asegurando así que los motores de búsqueda (como Google) puedan encontrarlas y rastrearlas. De hecho, un sitemap ayuda a los motores de búsqueda a entender la estructura de tu sitio web.

Imagínatelo como un mapa de tu sitio web. Éste muestra cuáles son todas las páginas de tu sitio web.

## Usando [gatsby-plugin-sitemap](/packages/gatsby-plugin-sitemap/)

Para generar un sitemap en XML, debes usar el paquete [`gatsby-plugin-sitemap`](/packages/gatsby-plugin-sitemap/).

Instala el paquete corriendo el siguiente comando:
`npm install --save gatsby-plugin-sitemap`

### Cómo configurarlo

Una vez que la instalación esté completa, podemos añadir este plugin a nuestro archivo de configuración `gatsby-config.js`, así:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    siteUrl: `https://www.ejemplo.com`
  },
  plugins: [`gatsby-plugin-sitemap`]
};
```

**Nota:** La propiedad siteUrl debe ser definida y no dejarse vacía.

Luego ejecuta un build (`npm run build`) ya que la generación del sitemap sucederá solamente en compilaciones de producción. ¡Esto es todo lo que se requiere para tener un sitemap funcional con Gatsby! Por defecto, la ruta del sitemap generado es /sitemap.xml e incluirá todas las páginas de tu sitio, pero obviamente, el plugin expone opciones para configurar esta funcionalidad por defecto.

### Modificaciones adicionales

Otras instrucciones para modificación se encuentran disponibles en la [documentación de `gatsby-plugin-sitemap`](/packages/gatsby-plugin-sitemap).

## Más información

- Mira también la publicación de [gatsby-plugin-advanced-sitemap](/blog/2019-05-07-advanced-sitemap-plugin-for-seo/) en el blog de Gatsby.
