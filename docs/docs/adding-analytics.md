---
title: Adición de análisis
---

## ¿Por qué usar el análisis?

Una vez que tenga su sitio en vivo, comenzará a querer tener una idea de cuántos visitantes están llegando a su sitio junto con otras métricas como:

- ¿Qué páginas son más populares?
- ¿De dónde vienen mis visitantes?
- ¿Cuándo visitan mi sitio?

Google Analytics proporciona una forma de recopilar estos datos y realizar análisis en ellos respondiendo a las preguntas anteriores, entre muchas otras. La plataforma es gratuita para 10 millones de visitas al mes por número de seguimiento. Hay otras opciones de análisis: consulte la sección «Otros complementos de análisis de Gatsby» en la parte inferior de este documento para ver ideas.

## Configuración de Google Analytics

El primer paso es configurar una cuenta de Google Analytics. Puedes hacerlo. [aquí](https://analytics.google.com/) iniciando sesión con tu cuenta de Google.

Google también tiene una [página de inicio](https://support.google.com/analytics/answer/1008015?hl=en) para referencia.

Una vez que tenga una cuenta, se le pedirá que configure una nueva propiedad. Esta propiedad tendrá un identificador de seguimiento asociado. En este caso la propiedad será la propia página web. Rellene el formulario con el nombre de su sitio web y la URL.

El identificador de seguimiento es el que se utiliza para identificar datos con el tráfico del sitio. Normalmente, usarías un identificador de seguimiento diferente para cada sitio web que estés supervisando.

Ahora debe tener un número de seguimiento; tome nota de ello, ya que su sitio web tendrá que hacer referencia al mismo cuando envíe vistas de páginas a Google Analytics. Debe tener el formato `UA-XXXXXXXXX-X`.

Puedes encontrar este identificador de seguimiento más adelante yendo a`Admin > Tracking Info > Tracking Code`.

## Uso `gatsby-plugin-google-analytics`

Ahora, es hora de configurar Gatsby para que envíe vistas de páginas a su cuenta de Google Analytics.

Vamos a usar `gatsby-plugin-google-analytics`. Para otras opciones de análisis (incluidos Google Analytics gtag.js y Google Tag Manager), consulte [other Gatsby analytics plugins](#other-gatsby-analytics-plugins).

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

> Nota: Lea más sobre [gatsby-config.js](/docs/gatsby-config/)

La documentación completa del plugin se puede encontrar [aquí](/packages/gatsby-plugin-google-analytics/).

Hay varias opciones de configuración adicionales, tanto con el complemento Gatsby como también en su cuenta de Google Analytics, para que pueda adaptar las cosas a las necesidades de su sitio web.

Una vez configurado, puede implementar su sitio para probar! Si navega a la página de inicio de Google Analytics, debería ver un panel con estadísticas diferentes.

## Otros complementos de análisis de Gatsby

- [Google Tag Manager](/packages/gatsby-plugin-google-tagmanager/)
- [Google Analytics gtag.js](/packages/gatsby-plugin-gtag/)
- [Segment](/packages/gatsby-plugin-segment-js)
- [Amplitude Analytics](/packages/gatsby-plugin-amplitude-analytics)
- [Fathom](/packages/gatsby-plugin-fathom/)
- [Baidu](/packages/gatsby-plugin-baidu-analytics/)
- [Matomo (formerly Piwik)](/packages/gatsby-plugin-matomo/)
- [Simple Analytics](/packages/gatsby-plugin-simple-analytics)
