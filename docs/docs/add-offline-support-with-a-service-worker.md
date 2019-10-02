---
title: Agregar soporte técnico sin conexión con un trabajador de servicio
---

Si ha ejecutado un [audit with Lighthouse](/docs/audit-with-lighthouse/), es posible que hayas notado una puntuación poco brillante en la categoría «Aplicación web progresiva». Vamos a abordar cómo puedes mejorar esa puntuación.

1.  Usted puede [add a manifest file](/docs/add-a-manifest-file/). Asegúrese de que el plugin de manifiesto aparece _before_ el plugin sin conexión para que el plugin sin conexión pueda almacenar en caché la `manifest.webmanifest`.

2.  También puede agregar soporte sin conexión, ya que otro requisito para que un sitio web califique como PWA es el uso de un [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API). [Gatsby's offline plugin](/packages/gatsby-plugin-offline/) hace que un sitio de Gatsby funcione sin conexión (y lo hace más resistente a las malas condiciones de red) mediante la creación de un trabajador de servicio para su sitio.

### ¿Qué es un trabajador de servicio?

Un trabajador de servicio es una secuencia de comandos que el explorador ejecuta en segundo plano, independiente de una página Web, abriendo la puerta a entidades que no necesitan una página Web o interacción del usuario. Aumentan la disponibilidad de su sitio en conexiones irregulares, y son esenciales para crear una agradable experiencia de usuario.

Es compatible con funciones como notificaciones push y sincronización en segundo plano.

### Usar trabajadores de servicio en Gatsby con `gatsby-plugin-offline`

Gatsby proporciona una interfaz de plugin impresionante para crear y cargar un trabajador de servicio en su sitio:
[gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Recomendamos usar este plugin junto con el[manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (No olvide enumerar el plugin sin conexión después del plugin de manifiesto para que el archivo de manifiesto se pueda incluir en el trabajador de servicio).

### Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Agregue este plugin a su `gatsby-config.js`

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        ...
      }
    },
    'gatsby-plugin-offline'
  ]
}
```

Eso es todo lo que necesita para agregar soporte sin conexión a su sitio de Gatsby.

Nota: El trabajador de servicio solo se registra en compilaciones de producción (`gatsby build`).

### Mostrar un mensaje cuando se actualiza un trabajador de servicio

Para mostrar un mensaje personalizado una vez que el trabajador de servicio encuentre una actualización, puede utilizar la herramienta [`onServiceWorkerUpdateReady`](/docs/browser-apis/#onServiceWorkerUpdateReady) API del navegador en su`gatsby-browser.js` archivo. El siguiente código mostrará un mensaje de confirmación preguntando al usuario si desea actualizar la página cuando se encuentre una actualización:

```javascript:title=gatsby-browser.js
export const onServiceWorkerUpdateReady = () => {
  const answer = window.confirm(
    `This application has been updated. ` +
      `Reload to display the latest version?`
  )

  if (answer === true) {
    window.location.reload()
  }
}
```

### Usar un trabajador de servicio personalizado en Gatsby

Puede agregar un trabajador de servicio personalizado si su caso de uso requiere algo que `gatsby-plugin-offline` no es compatible.

Agregue un archivo llamado `sw.js` en la `static` carpeta.

Utilice el comando [`registerServiceWorker`](/docs/browser-apis/#registerServiceWorker) en su archivo `gatsby-browser.js`.

```javascript:title=gatsby-browser.js
export const registerServiceWorker = () => true
```

¡Eso es todo! Gatsby registrará a su trabajador de servicio personalizado.

### Eliminación del trabajador de servicio

Si desea eliminar completamente el trabajador de servicio de su sitio, puede usar el complemento
`gatsby-plugin-remove-serviceworker` en lugar de`gatsby-plugin-offline`. ¿Ves [the README for `gatsby-plugin-offline`](/packages/gatsby-plugin-offline/#remove) para obtener instrucciones sobre cómo hacerlo.

## Referencias

- [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
