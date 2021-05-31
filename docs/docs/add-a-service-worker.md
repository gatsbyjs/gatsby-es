---
title: Añadiendo un Service Worker
---

### Qué es un _service worker_

Un _service worker_ es un script que el navegador ejecuta en segundo plano, aparte de la página web, abriendo la puerta a características que no necesitan una página web o la interacción del usuario. Incrementan la disponibilidad del sitio en conexiones irregulares, y son esenciales para crear una experiencia de usuario agradable.

Permite características como las notificaciones push o la sincronización en segundo plano.

### Usando _service workers_ en Gatsby con `gatsby-plugin-offline`

Gatsby provee un plugin maravilloso para crear y cargar un _service worker_ en tu sitio [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Puedes usar este plugin junto con el [plugin manifest](https://www.npmjs.com/package/gatsby-plugin-manifest). (No olvides listar el plugin offline después del plugin manifest para que el archivo manifest pueda ser incluido en el _service worker_).

### Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Añade este plugin a tu `gatsby-config.js`

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## Referencias

- [Introducción a los _service workers_](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/es/docs/Web/API/Service_Worker_API)
