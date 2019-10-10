---
title: Agregar soporte offline con un Service Worker
---

Si ha ejecutado una [auditoría con Lighthouse](/docs/audit-with-lighthouse/), Es posible que haya notado una puntuación mediocre en la categoría "Aplicación Web Progresiva". Veamos cómo puede mejorar esa puntuación.

1.  Puedes [agregar un archivo de manifiesto](/docs/add-a-manifest-file/). Asegúrese de que el Plugin de manifiesto aparezca en la lista _antes_ del Plugin offline para que el Puglin offline pueda almacenar en caché el creado `manifest.webmanifest`.
2.  También puede agregar soporte fuera de línea, ya que otro requisito para que un sitio web califique como PWA (Aplicación Web Progresiva por sus iniciales en inglés) es el uso de un [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API). [Gatsby's offline plugin](/packages/gatsby-plugin-offline/) hace que un sitio de Gatsby funcione sin conexión (Offline), y lo hace más resistente a las malas condiciones de la red, al crear un Service Worker para su sitio.

### Que es un Service Worker?

Un Service Worker es un script que su navegador ejecuta en segundo plano, separado de una página web, abriendo la puerta a funciones que no necesitan una página web o interacción del usuario. Aumentan la disponibilidad de su sitio en conexiones irregulares, y son esenciales para hacer una buena experiencia de usuario.

Admite características como notificaciones push y sincronización en segundo plano.

### Usar Service Workers en Gatsby con `gatsby-plugin-offline`

Gatsby proporciona un increíble Plugin de interfaces para crear y cargar un Service Worker en su sitio: [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Recomendamos usar este Plugin junto con el [manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). ( No olvide agregar el Plugin Offline después del Plugin de manifiesto para que el archivo de manifiesto se pueda incluir en el Service Worker).

### Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Agregue este Plugin en el archivo`gatsby-config.js`

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

Eso es todo lo que necesita para agregar soporte Offline a su sitio Gatsby.

Nota: el Service Worker solo se registra cuando se compila en producción(`gatsby build`).

### Mostrar un mensaje cuando un Service Worker se actualiza

Para mostrar un mensaje personalizado una vez que su Service Worker encuentre una actualización, puede usar el [`onServiceWorkerUpdateReady`](/docs/browser-apis/#onServiceWorkerUpdateReady) browser API en el archivo `gatsby-browser.js`. El siguiente código mostrará un mensaje de confirmación preguntando al usuario si desea actualizar la página cuando se encuentra una actualización:

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

### Usar un Service Worker personalizado en Gatsby

Puede agregar un Service Worker personalizado si su caso de uso requiere algo que `gatsby-plugin-offline` no soporta.

Agregar un archivo llamado `sw.js` en el fichero `static`.

Use el[`registerServiceWorker`](/docs/browser-apis/#registerServiceWorker) browser API en el archivo `gatsby-browser.js`.

```javascript:title=gatsby-browser.js
export const registerServiceWorker = () => true
```

That's all! Gatsby will register your custom service worker.

### Remover el Service Worker

Si desea eliminar por completo el Service Worker de su sitio, puede usar el Plugin `gatsby-plugin-remove-serviceworker` en lugar de `gatsby-plugin-offline`. Vea [el README de `gatsby-plugin-offline`](/packages/gatsby-plugin-offline/#remove) para obtener instrucciones sobre cómo hacer esto.

## Referencias

- [Service Workers: una Introducción](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
