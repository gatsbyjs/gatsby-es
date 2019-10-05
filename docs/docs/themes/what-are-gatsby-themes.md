---
El titulo: What Are Gatsby Themes?
---

Para introducir temas, vamos a caminar a través del viaje que condujo a la creación de temas.

Si alguna vez has creado un sitio de Gatsby completamente desde cero, sabes que hay una serie de decisiones que tomar. Tome, por ejemplo, creando un blog. Tiene que decidir donde sus datos vivirán, cómo tienen acceso a ellos, cómo son mostrados y diseñados, etc.

## Gatsby arrancadores

Uno existente para crear rápidamente Gatsby sitios con funcionalidad similar es usar "[Gatsby arrancadores](/docs/starters/)". Arrancadores son esencialmente Gatsby sitios con pre-funcionalidad configurada para un propósito en particular. Usted descarga un sitio completo de Gatsby, pre-construido para un propósito particular (por ejemplo, blogs, sitio de portafolio, etc.) y personalizar desde allí.

Estos arrancadores tradicionales da un primer paso hacia la reducción del nivel de esfuerzo involucrado en la creación de un nuevo sitio Gatsby. Sin embargo, hay dos problemas principales con los arrancadores tradicionales:

- Los sitios creados desde un tradicional motor de arranque han sido básicamente "expulsado" del motor de arranque -- No mantienen ninguna conexión con el arrancador, y comienzan a divergir inmediatamente. Si el inicio se actualiza más adelante, no hay una manera fácil de extraer los cambios ascendentes en un proyecto existente.
- Si creó varios sitios con el mismo inicio y más tarde deseaba realizar la misma actualización en todos esos sitios, tendría que hacerlos individualmente, sitio por sitio.

  ## Gatsby la plantilla

Introducir temas. Los temas de Gatsby permiten que la funcionalidad del sitio de Gatsby se empaque como un producto independiente para que otros (¡y usted mismo!) se reutilicen fácilmente. Usando un tradicional motor de arranque, toda su configuración predeterminada vidas directamente en su sitio. Usando un tema, toda su configuración de la falta vive en un paquete npm.

Las plantillas resuelven los problemas que experimentan los principiantes tradicionales:

- Los sitios creados mediante un Gatsby tema puede adoptar los cambios de flujo ascendente con el tema -- los temas son versionados paquetes que pueden actualizarse como cualquier otro paquete.
- Puede crear sitios múltiples que consumen el mismo tema. Para hacer actualizaciones a través de aquellos sitios, puede actualizar el tema central y darse un golpe en la versión con los sitios a través de archivos `package.json` (más bien que pasar el tiempo para actualizar aburridamente la funcionalidad de cada sitio individual).
- Los temas son compostables. Puede instalar un tema de blog junto con un tema de notas, junto con un tema de comercio electrónico (y así sucesivamente)

> Un tema de Gatsby es con eficacia Gatsby composable config. Proporcionan un enfoque de nivel más alto al funcionamiento con Gatsby que extractos lejos las partes complejas o reiterativas en un paquete reutilizable.

## ¿Y ahora qué?

- [Usando un Gatsby tema](/docs/themes/using-a-gatsby-theme)
- [Utilizando múltiples Gatsby temas](/docs/themes/using-multiple-gatsby-themes)
- [Construyendo temas](/docs/themes/building-themes)

## Publicaciones de blog relacionadas

Para un contexto adicional, echa un vistazo a las entradas de blog publicadas durante el desarrollo de temas:

- ¿[Por qué Temas?](/blog/2019-01-31-why-themes/)
- [Hoja de ruta de temas](/blog/2019-03-11-gatsby-themes-roadmap/)
- [Empezando con temas de Gatsby y MDX](/blog/2019-02-26-getting-started-with-gatsby-themes/)
- [Ver nosotros construir un tema directo](/blog/2019-02-11-gatsby-themes-livestream-and-example/)
- [Introduciendo temas de Gatsby por Chris Biscardi en días de Gatsby](https://www.gatsbyjs.com/gatsby-days-themes-chris/)
- [Ver todas las entradas de bitácora en temas](/blog/tags/themes)
