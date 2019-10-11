---
title: Adding analytics
---

## ¿Por qué usar métricas de análisis?

Cuando tienes tu sitio web preparado querrás saber cuantos visitantes van a entrar a tu sitio junto con otras métricas como:

- ¿Qué páginas son más populares?
- ¿De dónde proceden mis visitantes?
- ¿Cuándo visitan mi página?

Google Analytics provee una forma de recoger estos datos y analizarlos, respondiendo las preguntas de arriba junto con muchas otras. La plataforma es gratuita hasta 10 millones de entradas por mes e id de rastreo (Tracking ID). Hay otras opciones de métricas de análisis -- mira la sección "Otros plugins de Gatsby de análisis" de este documento en busca de ideas.

## Configurando Google Analytics

El primer paso es crear una cuenta de Google Analytics. Puedes hacerlo [aquí](https://analytics.google.com/) con tu cuenta de Google.

Google también tiene una [página de preparación](https://support.google.com/analytics/answer/1008015?hl=en) para más referencias.

Cuando tengas tu cuenta, te pedirá que añadas una nueva propiedad. Ésta propiedad tendrá un Tracking ID asociado. En este caso la propiedad será la página web en si misma. Rellena el formulario con el nombre de tu sitio web y URL.

El Tracking ID  es lo que se usa para identificar los datos con el tráfico de tu sitio web. Deberías usar un Tracking ID distinto para cada sitio web que estés monitorizando.

Deberías tener un Tracking ID; apúntalo, ya que tu sitio web necesitará referenciarlo cuando mande las visualizaciones de página a Google Analytics. Debería estar en formato `UA-XXXXXXXXX-X`.

Puedes encontrar el tracking ID posteriormente yendo a`Admin > Tracking Info > Tracking Code`.

## Usando `gatsby-plugin-google-analytics`

Ahora, es el momento de configurar Gatsby para enviar las visualizaciones de página a tu cuenta de Google Analytics.

Vamos a usar `gatsby-plugin-google-analytics`. Para otras opciones de métricas de análisis (incluyendo gtag.js de Google Analytics y Google Tag Manager), visita [otros plugins de métricas de análisis de Gatsby](#other-gatsby-analytics-plugins).

```shell
npm install --save gatsby-plugin-google-analytics
```

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-google-analytics`,
      options: {
        // replace "UA-XXXXXXXXX-X" with your own Tracking ID
        trackingId: "UA-XXXXXXXXX-X",
      },
    },
  ],
}
```

> Nota: Lee más sobre [gatsby-config.js](/docs/gatsby-config/)

La documentación completa para el plugin puede encontrarse [aquí](/packages/gatsby-plugin-google-analytics/).

Hay más opciones de configuración extra--tanto con el plugin de Gatsby como en tu cuenta de Google Analytics--así que puedes personalizar cosas para satisfacer las necesidades de tu página web.

¡Cuando esté configurado puedes desplegar tu sitio web para probar! Si navegas a la página de inicio de Google Analytics, deberías ver un tablero con diferentes estadísticas.

## Otros plugins de métricas de análisis de Gatsby

- [Google Tag Manager](/packages/gatsby-plugin-google-tagmanager/)
- [Google Analytics gtag.js](/packages/gatsby-plugin-gtag/)
- [Segment](/packages/gatsby-plugin-segment-js)
- [Amplitude Analytics](/packages/gatsby-plugin-amplitude-analytics)
- [Fathom](/packages/gatsby-plugin-fathom/)
- [Baidu](/packages/gatsby-plugin-baidu-analytics/)
- [Matomo (formerly Piwik)](/packages/gatsby-plugin-matomo/)
- [Simple Analytics](/packages/gatsby-plugin-simple-analytics)
