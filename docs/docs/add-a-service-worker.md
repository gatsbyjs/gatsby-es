---
title: Añadiendo un Service Worker
---

## What is a service worker

Un _service worker_ es un script que el navegador ejecuta en segundo plano, aparte de la página web, abriendo la puerta a características que no necesitan una página web o la interacción del usuario. Incrementan la disponibilidad del sitio en conexiones irregulares, y son esenciales para crear una experiencia de usuario agradable.

Permite características como las notificaciones push o la sincronización en segundo plano.

## Using service workers in Gatsby with `gatsby-plugin-offline`

Gatsby provee un plugin maravilloso para crear y cargar un _service worker_ en tu sitio [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

You can use this plugin together with the [manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (Don’t forget to list the offline plugin after the manifest plugin so that the manifest file can be included in the service worker).

## Installing `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Añade ese plugin a tu `gatsby-config.js`

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## Referencias

- [Introducción a los _service workers_](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/es/docs/Web/API/Service_Worker_API)
