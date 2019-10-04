# Gatsby en Español

This is the official Spanish translation of the Gatsby documentation.

# Gatsby en Español

This is the official Spanish translation of the Gatsby documentation.

<p align = "center">
  <a href="https://gatsbyjs.org">
    <img alt = "Gatsby" src = "https://www.gatsbyjs.org/monogram.svg" width = "60" />
  </a>
</p>
<h1 align = "center">
  Gatsby v2
</h1>

<h3 align = "center">
  ⚛️ 📄: cohete:
</h3>
<h3 align = "center">
  Rápido en todo lo que importa
</h3>
<p align = "center">
  Gatsby es un marco gratuito y de código abierto basado en React que ayuda a los desarrolladores a crear sitios web y aplicaciones increíblemente rápidos
</p>
<p align = "center">
  <a href="https://github.com/gatsbyjs/gatsby/blob/master/LICENSE">
    <img src = "https://img.shields.io/badge/license-MIT-blue.svg" alt = "Gatsby se libera bajo la licencia MIT". />
  </a>
  <a href="https://circleci.com/gh/gatsbyjs/gatsby">
    <img src = "https://circleci.com/gh/gatsbyjs/gatsby.svg?style=shield" alt = "Estado actual de construcción de CircleCI". />
  </a>
  <a href="https://www.npmjs.org/package/gatsby">
    <img src = "https://img.shields.io/npm/v/gatsby.svg" alt = "Versión actual del paquete npm". />
  </a>
  <a href="https://npmcharts.com/compare/gatsby?minimal=true">
    <img src = "https://img.shields.io/npm/dm/gatsby.svg" alt = "Descargas por mes en npm". />
  </a>
  <a href="https://npmcharts.com/compare/gatsby?minimal=true">
    <img src = "https://img.shields.io/npm/dt/gatsby.svg" alt = "Descargas totales en npm". />
  </a>
  <a href="https://gatsbyjs.org/contributing/how-to-contribute/">
    <img src = "https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt = "¡Bienvenidos PRs!" />
  </a>
  <a href="https://twitter.com/intent/follow?screen_name=gatsbyjs">
    <img src = "https://img.shields.io/twitter/follow/gatsbyjs.svg?label=Follow%20@gatsbyjs" alt = "Siga @gatsbyjs" />
  </a>
</p>

<h3 align = "center">
  <a href="https://gatsbyjs.org/docs/"> Inicio rápido </a>
  <span> · </span>
  <a href="https://gatsbyjs.org/tutorial/"> Tutorial </a>
  <span> · </span>
  <a href="https://gatsbyjs.org/plugins/"> Complementos </a>
  <span> · </span>
  <a href="https://gatsbyjs.org/starters/"> Starters </a>
  <span> · </span>
  <a href="https://gatsbyjs.org/showcase/"> Showcase </a>
  <span> · </span>
  <a href="https://gatsbyjs.org/contributing/how-to-contribute/"> Contribute </a>
  <span> · </span>
  Soporte: <a href="https://spectrum.chat/gatsby-js"> Spectrum </a>
  <span> & </span>
  <a href="https://gatsby.dev/discord"> Discordia </a>
</h3>

Gatsby es un marco web moderno para sitios web ultrarrápidos.

- ** Vaya más allá de los sitios web estáticos. ** Obtenga todos los beneficios de los sitios web estáticos sin ninguno de los
  limitaciones Los sitios de Gatsby son aplicaciones React completamente funcionales para que pueda crear de alta calidad,
  aplicaciones web dinámicas, desde blogs hasta sitios de comercio electrónico y paneles de usuario.

- ** Utilice una pila moderna para cada sitio. ** No importa de dónde provengan los datos, los sitios de Gatsby son
  construido usando React y GraphQL. Cree un flujo de trabajo uniforme para usted y su equipo, independientemente de
  si los datos provienen del mismo backend.

- ** Cargar datos desde cualquier lugar. ** Gatsby extrae datos de cualquier fuente de datos, ya sea Markdown
  archivos, un CMS sin cabeza como Contentful o WordPress, o una API REST o GraphQL. Usar complementos de origen
  para cargar sus datos, luego desarrolle usando la interfaz GraphQL uniforme de Gatsby.

- ** El rendimiento está horneado. ** As sus auditorías de rendimiento de forma predeterminada. Gatsby automatiza el código
  división, optimización de imágenes, inclusión de estilos críticos, carga diferida y captación previa de recursos,
  y más para garantizar que su sitio sea rápido, no se requiere ajuste manual.

- ** Host at Scale for Pennies. ** Los sitios Gatsby no requieren servidores, por lo que puedes alojar todo tu sitio
  sitio en un CDN por una fracción del costo de un sitio prestado por un servidor. Muchos sitios de Gatsby pueden ser
  alojado completamente gratis en servicios como GitHub Pages y Netlify.

[** Aprenda a usar Gatsby para su próximo proyecto. **] (https://gatsbyjs.org/docs/)

## ¿Qué hay en este documento?

- [Ponerse en marcha en 5 minutos] (# - levantarse y correr en 5 minutos)
- [Learning Gatsby] (# - aprendizaje-gatsby)
- [Guías de migración] (# - guías de migración)
- [Cómo contribuir] (# - cómo contribuir)
- [Licencia] (# memo-licencia)
- [Gracias a nuestros colaboradores y patrocinadores] (# - gracias a nuestros colaboradores y patrocinadores)

## 🚀 Ponte en marcha en 5 minutos

Puede obtener un nuevo sitio de Gatsby en funcionamiento en su entorno de desarrollo local en 5 minutos con estos cuatro pasos:

1. ** Instale la CLI de Gatsby. **

   ```shell
   npm install -g gatsby-cli
   ```

2. ** Cree un sitio Gatsby a partir de un iniciador Gatsby. **

   Configure su blog Gatsby en un solo comando:

   ```shell
   # crea un nuevo sitio Gatsby usando el iniciador predeterminado
   gatsby new my-blazing-fast-site
   ```

3. ** Inicie el sitio en modo `desarrollo`. **

   A continuación, vaya al directorio de su nuevo sitio e inícielo:

 
   ```shell
   cd my-blazing-fast-site/
   gatsby develop
   ```

4. ** ¡Abre el código fuente y comienza a editar! **

   Su sitio ahora se ejecuta en `http: // localhost: 8000`. Abra el directorio `my-blazing-fast-site` en el editor de código de su elección y edite` src / pages / index.js`. ¡Guarde sus cambios y el navegador se actualizará en tiempo real!

En este punto, tienes un sitio web de Gatsby completamente funcional.
