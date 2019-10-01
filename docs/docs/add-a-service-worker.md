---
title: Agregar un trabajador de servicio
---

### ¿Qué es un trabajador de servicio?

Un trabajador de servicio es un script que su navegador ejecuta en segundo plano, separado de una página web, abriendo la puerta a funciones que no necesitan una página web o interacción del usuario. Aumentan la disponibilidad de su sitio en conexiones irregulares, y son esenciales para hacer una buena experiencia de usuario.

Es compatible con funciones como notificaciones push y sincronización de fondo.

### Uso de trabajadores de servicio en Gatsby con `gatsby-plugin-offline`

Gatsby proporciona una increíble interfaz de complementos para crear y cargar un trabajador de servicio en su sitio [gatsby-plugin-offline] (https://www.npmjs.com/package/gatsby-plugin-offline).

Recomendamos utilizar este complemento junto con el [complemento de manifiesto] (https://www.npmjs.com/package/gatsby-plugin-manifest). (No olvide enumerar el complemento sin conexión después del complemento de manifiesto para que el archivo de manifiesto se pueda incluir en el trabajador de servicio).

### Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Agregue este complemento a su `gatsby-config.js`

`` `javascript: title = gatsby-config.js
complementos: [`gatsby-plugin-offline`]
`` `

## Referencias

- [Service Workers: an Introduction] (https://developers.google.com/web/fundamentals/primers/service-workers/)
- [API de Service Worker] (https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)