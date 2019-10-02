---
title: Agregar un trabajador de servicio
---

### ¿Qué es un trabajador de servicio?

Un trabajador de servicio es una secuencia de comandos que el explorador ejecuta en segundo plano, independiente de una página Web, abriendo la puerta a entidades que no necesitan una página Web o interacción del usuario. Aumentan la disponibilidad de su sitio en conexiones irregulares, y son esenciales para crear una agradable experiencia de usuario.

Es compatible con funciones como notificaciones push y sincronización en segundo plano.

### Usando trabajadores de servicio en Gatsby con `gatsby-plugin-offline`

Gatsby proporciona una interfaz de plugin impresionante para crear y cargar un trabajador de servicio en su sitio
[gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Recomendamos usar este plugin junto con el[manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (No olvide enumerar el complemento sin conexión después del plugin de manifiesto para que el archivo de manifiesto se pueda incluir en el trabajador de servicio).

### Instalando `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Agregue este plugin a su `gatsby-config.js`

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## Referencias

- [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
