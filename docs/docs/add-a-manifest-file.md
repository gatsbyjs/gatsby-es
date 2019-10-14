---
title: Añadir un archivo de manifiesto
---

Si has llevado a cabo una [auditoría con Lighthouse](/docs/audit-with-lighthouse/), puedes haberte dado cuenta de una puntuación un tanto mediocre en la categoría "Aplicación Web Progresiva" ("Progressive Web App"). Veamos como se puede mejorar esta puntuación.

Pero primero, ¿qué _son_ exactamente las PWA?

Son sitios web corrientes que aprovechan la funcionalidad de los navegadores web modernos para mejorar la experiencia web con características y beneficios similares a las aplicaciones. Visita [la visión general de Google](https://developers.google.com/web/progressive-web-apps/) que define una experiencia PWA y [la documentación sobre Aplicaciones Web Progresivas (PWAs)](/docs/progressive-web-app/) para aprender como un sitio Gatsby es una Aplicación Web Progresiva.

La inclusión de un archivo de manifiesto de aplicación web, es uno de los tres [requisitos base para una PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1) generalmente aceptados.

Citando a [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> El archivo de manifiesto de aplicación web es un archivo JSON simple que informa al navegador acerca de su aplicación web y como se debe comportar cuando sea 'instalada' en el dispositivo móvil o escritorio del usuario.

[El plugin de manifiesto de Gatsby](/packages/gatsby-plugin-manifest/) configura Gatsby para crear un archivo `manifest.webmanifest` en cada sitio construido.

### Usando `gatsby-plugin-manifest`

1.  Instala el plugin:

```shell
npm install --save gatsby-plugin-manifest
```

2. Añade un 'favicon' a tu aplicación en `src/images/icon.png`. El icono es necesario para construir todas las imágenes para el archivo de manifiesto. Para más información, visita la documentación en [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Añade el plugin al _array_ de `plugins` en tu fichero `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: "GatsbyJS",
        short_name: "GatsbyJS",
        start_url: "/",
        background_color: "#6b37bf",
        theme_color: "#6b37bf",
        // Habilita la opción "Añadir a pantalla de inicio" y deshabilita la interfaz de usuario del navegador (incluyendo el botón para ir atrás). 
        // Mira: https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: "standalone",
        icon: "src/images/icon.png", // Esta ruta es relativa a la raíz del sitio
        // Un atributo opcional que proporciona soporte para las comprobaciones CORS.
        // Si no provees ninguna opción crossOrigin, se omite CORS para el manifiesto.
        // Cualquier palabra inválida o cadena de texto vacía se interpreta como el valor `anonymous`
        crossOrigin: `use-credentials`,
      },
    },
  ]
}
```

Eso es todo lo que necesitas para empezar a añadir un manifiesto web a un sitio Gatsby. El ejemplo proporcionado refleja una configuración base -- visita la [documentación de referencia del plugin](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) para más opciones.