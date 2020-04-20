---
title: Hoja de trucos
---

El equipo de Gatsby ha creado un recurso que te puede ser útil al crear un sitio de Gatsby: ¡una hoja de trucos con todos los comandos principales y consejos de desarrollo!. Si lo deseas, descarga e imprime una copia (¡y pégala en tu estación de trabajo!). Para más información relacionada, visita [Inicio rápido](/docs/quick-start/) y [Comandos (Gatsby CLI)](/docs/gatsby-cli/).

Obtén el PDF: <a href="/gatsby-cheat-sheet.pdf" download>gatsby-cheat-sheet.pdf</a>

<figure aria-labelledby="cheat_sheet-text">
    <h2>Página 1</h2>
    <a href="/cheat-sheet_page_1.png" title="Click to open image in a new window" target="_blank" style="display:block;">
        <img src="/cheat-sheet_page_1.png" alt="Cheat Sheet - page 1" style="display:block; margin:0;" />
    </a>
    <h2>Página 2</h2>
    <a href="/cheat-sheet_page_2.png" title="Click to open image in a new window" target="_blank" style="display:block;">
        <img src="/cheat-sheet_page_2.png" alt="Cheat Sheet - page 2" style="display:block; margin:0;" />
    </a>
</figure>
<div
  id="cheat_sheet-text"
  style=" position: absolute; height: 1px; width: 1px;overflow: hidden; clip: rect(1px, 1px, 1px, 1px);"
>
  <h2>Contenidos de la hoja de trucos de Gatsby</h2>
  <p>
    v1.0 para Gatsby 2.x
    <a href="https://gatsby.dev/cheatsheet">
      Versión más reciente <span aria-hidden="true">↗</span>
    </a>
  </p>
  <h2>Documentación principal</h2>
  <table>
    <tbody>
      <tr>
        <td>
          <p>Documentación de Gatsby</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/docs">gatsby.dev/docs</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Gatsby en GitHub</p>
        </td>
        <td>
          <p>
            <a href="https://github.com/gatsbyjs/gatsby">
              github.com/gatsbyjs/gatsby
            </a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Tutorial de Gatsby</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            Inicio Rápido
            <br />
            (para desarrolladores intermedios y avanzados)
          </p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/quick-start">gatsby.dev/quick-start</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Starters de Gatsby</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/starters">gatsby.dev/starters</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Guía de referencia rápida</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/recipes">gatsby.dev/recipes</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Agregando imágenes</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/image">gatsby.dev/image</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>APIs Node de Gatsby</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/api">gatsby.dev/api</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Consultando con GraphQL</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/graphql">gatsby.dev/graphql</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Desplegando y Alojando</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/deploy">gatsby.dev/deploy</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Usando Gatsby Link</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/link">gatsby.dev/link</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Query estático</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/static-query">
              gatsby.dev/static-query
            </a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Como contribuir</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/contribute">gatsby.dev/contribute</a>
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  <p>
    <a href="https://www.gatsbyjs.org/">gatsbyjs.org</a>
  </p>
  <p>
    <a href="https://twitter.com/gatsbyjs">twitter.com/gatsbyjs</a>
  </p>
  <h2>Comandos del CLI de Gatsby</h2>
  <p>
    Primero, instala el ejecutable global:
    <br />
    <code>npm install -g gatsby-cli</code>
  </p>
  <p>
    Ejecuta <code>gatsby --help</code> para obtener uns lista de comandos y opciones.
  </p>
  <h3>
    <code>
      gatsby new <span style="font-weight:normal">my-site-name</span>
    </code>
  </h3>
  <p>
    Crea un nuevo sitio local de Gatsby usando el starter por defecto (mira "Comandos
    de inicio rápido" en esta hoja de trucos para ver como usar otros starters).
  </p>
  <h3>
    <code>gatsby develop</code>
  </h3>
  <p>Inicia el servidor de desarrollo de Gatsby.</p>
  <table>
    <tbody>
      <tr>
        <td>
          <p>
            <code>-H, --host</code>
          </p>
        </td>
        <td>
          <p>
            Configura el host. Predeterminado a <code>localhost</code>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>-p, --port</code>
          </p>
        </td>
        <td>
          <p>
            Configura el puerto. Predeterminado a env.PORT o <code>8000</code>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>-o, --open</code>
          </p>
        </td>
        <td>
          <p>Abre el sitio en tu navegador (por defecto)</p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>-S, --https</code>
          </p>
        </td>
        <td>
          <p>Usar HTTPS</p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>
    <code>gatsby build</code>
  </h3>
  <p>
    Compila tu aplicación y la deja lista para desplegar.
    <br />
  </p>
  <table>
    <tbody>
      <tr>
        <td>
          <p>
            <code>--prefix-paths</code>
          </p>
        </td>
        <td>
          <p>
            Compila el sitio con rutas predeterminadas
            <br />
            (agrega o cambia <code>pathPrefix</code> en tu configuración)
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>--no-uglify</code>
          </p>
        </td>
        <td>
          <p>
            Compila el sitio sin aplicar "uglify" al compilado de JS
            <br />
            (para depuración)
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>--open-tracing-config-file</code>
          </p>
        </td>
        <td>
          <p>
            Archivo de configuración para trazador (compatible con OpenTracing). Mira{" "}
            <a href="https://gatsby.dev/tracing">gatsby.dev/tracing</a>
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>
    <code>gatsby serve</code>
  </h3>
  <p>Sirve el compilado de producción para pruebas.</p>
  <table>
    <tbody>
      <tr>
        <td>
          <p>
            <code>-H, --host</code>
          </p>
        </td>
        <td>
          <p>
            Configura el host. Predeterminado a <code>localhost</code>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>-p, --port</code>
          </p>
        </td>
        <td>
          <p>
            Configura el puerto. Predeterminado a <code>9000</code>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>-o, --open</code>
          </p>
        </td>
        <td>
          <p>Abre el sitio en tu navegador (por defecto)</p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>--prefix-paths</code>
          </p>
        </td>
        <td>
          <p>
            Sirve el sitio con rutas predeterminadas (si fue compilado con{" "}
            <code>pathPrefix</code> en tu <code>gatsby-config.js</code>)
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>
    <code>gatsby info</code>
  </h3>
  <p>
    Obtiene información de ayuda del ambiente que será requerida cuando se reporte un
    error a{" "}
    <a href="https://github.com/gatsbyjs/gatsby/issues">
      github.com/gatsbyjs/gatsby/issues
    </a>
    .
  </p>
  <table>
    <tbody>
      <tr>
        <td>
          <p>
            <code>-C, --clipboard</code>
          </p>
        </td>
        <td>
          <p>Copia automáticamente la información del ambiente al portapapeles</p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>gatsby clean</h3>
  <p>
    Borra completamente los directorios de <code>.cache</code> y <code>public</code> de Gatsby.
  </p>
  <h2>¡Camisetas, sombreros, sudaderas y más!</h2>
  <p>
    ¡Registrate al boletín informativo de Gatsby y obtén <strong>30% de descuento</strong> en
    tu compra de la tienda de Gatsby! (
    <a href="https://gatsby.dev/store">gatsby.dev/store</a>)
  </p>
  <p>
    Registrate en <a href="https://gatsby.dev/discount">gatsby.dev/discount</a>
  </p>
  <h2>Comandos de inicio rápido</h2>
  <p>
    Crea un nuevo sitio de Gatsby usando el starter de “Blog”:
    <br />
    <code>
      gatsby new my-blog-starter https://github.com/gatsbyjs/gatsby-starter-blog
    </code>
  </p>
  <p>
    Navega al directorio de tu nuevo sitio y lo inicia:
    <br />
    <code>
      cd my-blog-starter/
      <br />
      gatsby develop
    </code>
  </p>
  <p>
    ¡Tu sitio sé está ejecutando en <code>http://localhost:8000</code>!
  </p>
  <p>
    {/* prettier-ignore */}
    También veras un segundo enlace: <code>http://localhost:8000/___graphql</code>.
    Esto es una herramienta que puedes usar para experimentar consultando tus datos. Aprende más
    sobre ella en <a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a>
  </p>
  <p>
    Para más starters de Gatsby, visita{" "}
    <a href="https://gatsby.dev/starters">gatsby.dev/starters</a>.
  </p>
  <h2>Definiciones de archivos útiles</h2>
  <p>
    Cada uno de estos archivos debe vivir en la carpeta raíz de tu proyecto de Gatsby.
    Mira <a href="https://gatsby.dev/projects">gatsby.dev/projects</a>
  </p>
  <p>
    <code>gatsby-config.js</code> — opciones de configuración para un sitio de Gatsby, con
    metadatos para el título, descripción y plugins del proyecto, entre otros.
  </p>
  <p>
    <code>gatsby-node.js</code> — implementa APIs de Node.js de Gatsby para personalizar
    y extender la configuración por defecto, afectando el proceso de compilado
  </p>
  <p>
    <code>gatsby-browser.js</code> — personaliza y extiende la configuración por defecto
    afectando el navegador, usando las APIs de navegador de Gatsby
  </p>
  <p>
    <code>gatsby-ssr.js</code> — usa las APIs de renderizado en servidor de Gatsby para
    personalizar la configuración por defecto afectando el renderizado en servidor
  </p>
</div>
