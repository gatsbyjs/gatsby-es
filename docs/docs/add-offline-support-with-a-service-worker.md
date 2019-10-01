---
title: Agregar soporte sin conexión con un trabajador de servicio
---

Si ha ejecutado una [auditoría con Lighthouse] (/ docs / audit-with-lighthouse /), es posible que haya notado una puntuación mediocre en la categoría "Aplicación web progresiva". Veamos cómo puedes mejorar esa puntuación.

1. Puede [agregar un archivo de manifiesto] (/ docs / add-a-manifest-file /). Asegúrese de que el complemento de manifiesto esté en la lista _antes_ del complemento sin conexión para que el complemento sin conexión pueda almacenar en caché el `manifest.webmanifest` creado.
2. También puede agregar soporte fuera de línea, ya que otro requisito para que un sitio web califique como PWA es el uso de un [trabajador de servicio] (https://developer.mozilla.org/en-US/docs/Web/API/ Service_Worker_API). [El complemento sin conexión de Gatsby] (/ packages / gatsby-plugin-offline /) hace que un sitio de Gatsby funcione sin conexión, y lo hace más resistente a las malas condiciones de la red, al crear un trabajador de servicio para su sitio.

### ¿Qué es un trabajador de servicio?

Un trabajador de servicio es un script que su navegador ejecuta en segundo plano, separado de una página web, abriendo la puerta a funciones que no necesitan una página web o interacción del usuario. Aumentan la disponibilidad de su sitio en conexiones irregulares, y son esenciales para hacer una buena experiencia de usuario.

Admite características como notificaciones push y sincronización de fondo.

### Uso de trabajadores de servicio en Gatsby con `gatsby-plugin-offline`

Gatsby proporciona una increíble interfaz de complemento para crear y cargar un trabajador de servicio en su sitio: [gatsby-plugin-offline] (https://www.npmjs.com/package/gatsby-plugin-offline).

Recomendamos utilizar este complemento junto con el [complemento de manifiesto] (https://www.npmjs.com/package/gatsby-plugin-manifest). (No olvide enumerar el complemento sin conexión después del complemento de manifiesto para que el archivo de manifiesto se pueda incluir en el trabajador de servicio).

### Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Agregue este complemento a su `gatsby-config.js`

`` `javascript: title = gatsby-config.js
{
  complementos: [
    {
      resolver: `gatsby-plugin-manifest`,
      opciones: {
        ...
      }
    },
    'gatsby-plugin-offline'
  ]
}
`` `

Eso es todo lo que necesita para agregar soporte fuera de línea a su sitio Gatsby.

Nota: El trabajador de servicio solo se registra en las compilaciones de producción (`gatsby build`).

### Mostrar un mensaje cuando un trabajador de servicio se actualiza

Para mostrar un mensaje personalizado una vez que su trabajador de servicio encuentre una actualización, puede usar la API del navegador [`onServiceWorkerUpdateReady`] (/ docs / browser-apis / # onServiceWorkerUpdateReady) en su archivo` gatsby-browser.js`. El siguiente código mostrará un mensaje de confirmación preguntando al usuario si desea actualizar la página cuando se encuentra una actualización:

`` `javascript: title = gatsby-browser.js
export const onServiceWorkerUpdateReady = () => {
  respuesta const = window.confirm (
    `Esta aplicación ha sido actualizada. `+
      `¿Recargar para mostrar la última versión?`
  )

  if (respuesta === verdadero) {
    window.location.reload ()
  }
}
`` `

### Uso de un trabajador de servicio personalizado en Gatsby

Puede agregar un trabajador de servicio personalizado si su caso de uso requiere algo que no sea compatible con `gatsby-plugin-offline`.

Agregue un archivo llamado `sw.js` en la carpeta` static`.

Utilice la API del navegador [`registerServiceWorker`] (/ docs / browser-apis / # registerServiceWorker) en su archivo` gatsby-browser.js`.

`` `javascript: title = gatsby-browser.js
export const registerServiceWorker = () => true
`` `

¡Eso es todo! Gatsby registrará a su trabajador de servicio personalizado.

### Eliminando al trabajador del servicio

Si desea eliminar completamente al trabajador de servicio de su sitio, puede usar el complemento `gatsby-plugin-remove-serviceworker` en lugar de` gatsby-plugin-offline`. Consulte [el archivo README para `gatsby-plugin-offline`] (/ packages / gatsby-plugin-offline / # remove) para obtener instrucciones sobre cómo hacerlo.

## Referencias

- [Service Workers: an Introduction] (https://developers.google.com/web/fundamentals/primers/service-workers/)
- [API de Service Worker] (https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)