---
Título: Agregar análisis
---

## ¿Por qué usar análisis?

Una vez que tenga su sitio activo, comenzará a querer tener una idea de cuántos visitantes vienen a su sitio junto con otras métricas como:

- ¿Qué páginas son las más populares?
- ¿De dónde vienen mis visitantes?
- ¿Cuándo visitan las personas mi sitio?

Google Analytics proporciona una forma de recopilar estos datos y realizar análisis sobre ellos respondiendo las preguntas anteriores, entre muchos otros. La plataforma es gratuita por 10 millones de visitas al mes por ID de seguimiento. Hay otras opciones de análisis: consulte la sección "Otros complementos de análisis de Gatsby" al final de este documento para obtener ideas.

## Configuración de Google Analytics

El primer paso es configurar una cuenta de Google Analytics. Puede hacerlo [aquí] (https://analytics.google.com/) iniciando sesión con su cuenta de Google.

Google también tiene una [página de inicio] (https://support.google.com/analytics/answer/1008015?hl=es) como referencia.

Una vez que tenga una cuenta, se le pedirá que configure una nueva propiedad. Esta propiedad tendrá un ID de seguimiento asociado. En este caso, la propiedad será el propio sitio web. Complete el formulario con el nombre y la URL de su sitio web.

El ID de seguimiento es lo que se utiliza para identificar datos con el tráfico de su sitio. Por lo general, usaría una ID de seguimiento diferente para cada sitio web que esté monitoreando.

Ahora debe tener una identificación de seguimiento; tome nota de ello, ya que su sitio web deberá hacer referencia a él cuando envíe vistas de página a Google Analytics. Debe estar en el formato `UA-XXXXXXXXX-X`.

Puede encontrar esta identificación de seguimiento más adelante yendo a `Admin> Información de seguimiento> Código de seguimiento`.

## Usando `gatsby-plugin-google-analytics`

Ahora es el momento de configurar Gatsby para enviar visitas a la página a su cuenta de Google Analytics.

Vamos a usar `gatsby-plugin-google-analytics`. Para otras opciones de análisis (incluidos Google Analytics gtag.js y Google Tag Manager), marque [otros complementos de análisis de Gatsby] (# other-gatsby-analytics-plugins).

`` `concha
npm install --save gatsby-plugin-google-analytics
`` `

`` `js: title = gatsby-config.js
module.exports = {
  complementos: [
    {
      resolver: `gatsby-plugin-google-analytics`,
      opciones: {
        // reemplaza "UA-XXXXXXXXX-X" con tu propia ID de seguimiento
        trackingId: "UA-XXXXXXXXX-X",
      },
    },
  ],
}
`` `
> Nota: Lea más sobre [gatsby-config.js] (/ docs / gatsby-config /)

Se puede encontrar la documentación completa del complemento [aquí] (/ packages / gatsby-plugin-google-analytics /).

Hay varias opciones de configuración adicionales, tanto con el complemento Gatsby como en su cuenta de Google Analytics, para que pueda adaptar las cosas a las necesidades de su sitio web.

Una vez que esté configurado, puede implementar su sitio para probar. Si navega a la página de inicio de Google Analytics, debería ver un panel con estadísticas diferentes.

## Otros complementos de análisis de Gatsby

- [Administrador de etiquetas de Google] (/ packages / gatsby-plugin-google-tagmanager /)
- [Google Analytics gtag.js] (/ packages / gatsby-plugin-gtag /)
- [Segmento] (/ packages / gatsby-plugin-segmento-js)
- [Análisis de amplitud] (/ packages / gatsby-plugin-amplitude-analytics)
- [Fathom] (/ packages / gatsby-plugin-fathom /)
- [Baidu] (/ packages / gatsby-plugin-baidu-analytics /)
- [Matomo (anteriormente Piwik)] (/ packages / gatsby-plugin-matomo /)
- [Simple Analytics] (/ packages / gatsby-plugin-simple-analytics)