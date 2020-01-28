---
title: Typography.js
---

## Uso de Typography.js en Gatsby

Typography.js es una biblioteca de JavaScript que te permite explorar el diseño tipográfico de tu sitio web y definir hermosos temas tipográficos personalizados y preexistentes. Esta librería te permite cambiar la fuente en tu sitio web con facilidad. Actualmente, Typography.js mantiene más de 30 temas para tu uso. También puedes crear tus propios temas de fuentes personalizados si no hay temas disponibles que se ajusten a tus requisitos. Para usar Typography en tu proyecto, deberás instalar un [plugin de Gatsby](https://www.gatsbyjs.org/packages/gatsby-plugin-typography/) y especificar un objeto de configuración para Typography.

## Instalación del plugin Typography

Gatsby tiene el plugin `gatsby-plugin-typography` para integrar Typography.js a tu proyecto.

Puedes instalar el plugin y sus dependencias en tu proyecto, ejecutando el comando `npm install gatsby-plugin-typography react-typography typography --save`

Una vez completada la instalación del plugin, navega hasta el archivo `gatsby-config.js` ubicado en la raíz del directorio de tu proyecto y agrega el complemento a la configuración:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
    // highlight-end
  ],
}
```

Puedes especificar dos opciones para `gatsby-plugin-typography`:

- **pathToConfigModule** (string): La ruta al archivo donde exportas tu configuración de Typography.
- **omitGoogleFont** (boolean, `default: false`): De forma predeterminada, Typography incluye un asistente que realiza una solicitud al CDN de Google Fonts para las fuentes que necesites. Puede que quieras utilizar tus propias fuentes, ya sea inyectando fuentes o utilizando un CDN de tu elección. Al configurar `omitGoogleFont: true`, `gatsby-plugin-typography` omitirá agregar el ayudante de fuente. En su lugar, deberás incluir las fuentes apropiadas tú mismo - dirígete a [Agregar una fuente local](https://www.gatsbyjs.org/docs/recipes/#adding-a-local-font)

## Crear la configuración de Typography

Después de haber agregado el plugin, crea el directorio `src/utils/`, si aún no existe en tu proyecto, y agrega un nuevo archivo llamado `typography.js`. Utilizarás este archivo para especificar la configuración de Typography y lo establecerás como la ruta para la opción `pathToConfigModule`.

Dentro del archivo `typography.js` que creaste, define la configuración de tipografía de tu sitio web. Una configuración básica de typography.js luce así:

```js:title=src/utils/typography.js
import Typography from "typography"

const typography = new Typography({
  baseFontSize: "18px",
  baseLineHeight: 1.666,
  headerFontFamily: [
    "Avenir Next",
    "Helvetica Neue",
    "Segoe UI",
    "Helvetica",
    "Arial",
    "sans-serif",
  ],
  bodyFontFamily: ["Georgia", "serif"],
})

export default typography
```

Si estás instalando Typography.js en un proyecto Gatsby existente que has comenzado, tendrás que eliminar de tu base de código todos los estilos de fuente CSS conflictivos, en favor de tu nueva configuración Typography.js.

Los tamaños de fuente de todos los elementos en Typography.js crecen y se reducen en relación con el valor de `baseFontSize` definido anteriormente. Intenta jugar con este valor y observa la diferencia visual que puede causar en tu sitio web.

Para buscar o crear un nuevo tema de tipografía, puedes visitar [Typography.js](https://kyleamathews.github.io/typography.js/) para ver una lista de opciones.

## Installing Typography themes

Typography.js tiene temas incorporados que pueden ahorrarTE tiempo al definir el estilo de fuente de tu sitio web. El tema Funston, mantenido por Typography, es uno de los temas integrados. Para instalar el tema Funston desde npm, ejecuta el comando: `npm install typography-theme-funston --save`

Para usar el tema, edita el archivo `typography.js` que creaste anteriormente y hazle saber a Typography de la nueva configuración:

```diff:title=src/utils/typography.js
import Typography from "typography";
// highlight-start
+ import funstonTheme from 'typography-theme-funston'
// highlight-end
const typography = new Typography(
- {
-     baseFontSize: '18px',
-     baseLineHeight: 1.666,
-     headerFontFamily: ['Avenir Next', 'Helvetica Neue', 'Segoe UI', 'Helvetica', 'Arial', 'sans-serif'],
-     bodyFontFamily: ['Georgia', 'serif'],
- },
// highlight-start
+ funstonTheme
// highlight-end
);

export default typography;
```

Después de completar los pasos anteriores, podrás iniciar el servidor de desarrollo utilizando el comando `gatsby develop` y navegar al sitio web local `http://localhost:8000`. Si todo salió bien, deberías poder ver el texto en tu sitio web utilizando el tema tipográfico Funston.

**Nota**: Si tus fuentes permanecen sin cambios, elimina todas las referencias a `font-family` de tu CSS y verifica nuevamente.

Para encontrar más temas para instalar, consulta el sitio web oficial de [Typography.js](https://kyleamathews.github.io/typography.js/).
