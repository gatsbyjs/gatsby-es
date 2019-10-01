---
título: Agregar un archivo de manifiesto
---

Si ha ejecutado una [auditoría con Lighthouse] (/ docs / audit-with-lighthouse /), es posible que haya notado una puntuación mediocre en la categoría "Aplicación web progresiva". Veamos cómo puedes mejorar esa puntuación.

Pero primero, ¿qué son exactamente los PWA?

Son sitios web regulares que aprovechan la funcionalidad moderna del navegador para aumentar la experiencia web con características y beneficios similares a las aplicaciones. Consulte [Descripción general de Google] (https://developers.google.com/web/progressive-web-apps/) de lo que define una experiencia PWA y el [Documento de aplicaciones web progresivas (PWA)] (/ docs /gressive-web -app /) para aprender cómo un sitio de Gatsby es una aplicación web progresiva.

La inclusión de un manifiesto de aplicación web es uno de los tres generalmente aceptados [requisitos de línea de base para un PWA] (https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1) .

Citando [Google] (https://developers.google.com/web/fundamentals/web-app-manifest/):

> El manifiesto de la aplicación web es un simple archivo JSON que le informa al navegador sobre su aplicación web y cómo debe comportarse cuando se 'instala' en el dispositivo móvil o escritorio del usuario.

[El complemento de manifiesto de Gatsby] (/ packages / gatsby-plugin-manifest /) configura Gatsby para crear un archivo `manifest.webmanifest` en cada compilación del sitio.

### Usando `gatsby-plugin-manifest`

1. Instale el complemento:

`` `concha
npm install --save gatsby-plugin-manifest
`` `

2. Agregue un favicon para su aplicación en `src / images / icon.png`. El icono es necesario para construir todas las imágenes para el manifiesto. Para obtener más información, consulte los documentos de [`gatsby-plugin-manifest`] (https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Agregue el complemento a la matriz `plugins` en su archivo` gatsby-config.js`.

`` `javascript: title = gatsby-config.js
{
  complementos: [
    {
      resolver: `gatsby-plugin-manifest`,
      opciones: {
        nombre: "GatsbyJS",
        nombre_corto: "GatsbyJS",
        start_url: "/",
        background_color: "# 6b37bf",
        theme_color: "# 6b37bf",
        // Activa el mensaje "Agregar a la pantalla de inicio" y desactiva la interfaz de usuario del navegador (incluido el botón Atrás)
        // ver https://developers.google.com/web/fundamentals/web-app-manifest/#display
        pantalla: "independiente",
        icon: "src / images / icon.png", // Esta ruta es relativa a la raíz del sitio.
        // Un atributo opcional que proporciona soporte para la verificación CORS.
        // Si no proporciona una opción crossOrigin, omitirá CORS para el manifiesto.
        // Cualquier palabra clave inválida o cadena vacía por defecto es `anónimo`
        crossOrigin: `use-credentials`,
      },
    },
  ]
}
`` `

Eso es todo lo que necesita para comenzar a agregar un manifiesto web a un sitio de Gatsby. El ejemplo dado refleja una configuración básica: consulte la [referencia del complemento] (/ packages / gatsby-plugin-manifest /? = Gatsby-plugin-manifest # modo automático) para obtener más opciones.