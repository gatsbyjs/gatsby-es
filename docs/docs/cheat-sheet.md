---
title: Hoja de trucos
---

El equipo de Gatsby ha creado un recurso que te puede ser útil al crear un sitio de Gatsby: ¡una hoja de trucos con todos los comandos principales y consejos de desarrollo!. Si lo deseas, descarga e imprime una copia (¡y pégala en tu estación de trabajo!). Para más información relacionada, visita [Inicio rápido](/docs/quick-start/) y [Comandos (Gatsby CLI)](/docs/gatsby-cli/).

Obtén el PDF: <a href="/gatsby-cheat-sheet.pdf" download>gatsby-cheat-sheet.pdf</a>

<figure aria-labelledby="cheat_sheet-text">
<<<<<<< HEAD
    <h2>Página 1</h2>
    <a href="/cheat-sheet_page_1.png" title="Click to open image in a new window" target="_blank" style="display:block;">
        <img src="/cheat-sheet_page_1.png" alt="Cheat Sheet - page 1" style="display:block; margin:0;" />
    </a>
    <h2>Página 2</h2>
    <a href="/cheat-sheet_page_2.png" title="Click to open image in a new window" target="_blank" style="display:block;">
        <img src="/cheat-sheet_page_2.png" alt="Cheat Sheet - page 2" style="display:block; margin:0;" />
    </a>
</figure>

<div id="cheat_sheet-text" style=" position: absolute; height: 1px; width: 1px;overflow: hidden; clip: rect(1px, 1px, 1px, 1px);">
    <h2>Contenidos de la hoja de trucos de Gatsby</h2>
    <p>v1.0 para Gatsby 2.x
        <a href="https://gatsby.dev/cheatsheet">Última versión <span aria-hidden="true">↗</span></a>
    </p>
    <h2>Docs principales</h2>
    <table>
        <tbody>
            <tr>
                <td>
                    <p>Docs Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/docs">gatsby.dev/docs</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Gatsby en GitHub</p>
                </td>
                <td>
                    <p><a href="https://github.com/gatsbyjs/gatsby">github.com/gatsbyjs/gatsby</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Tutorial de Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Inicio Rápido<br />(para desarrolladores intermedios y avanzados)</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/quick-start">gatsby.dev/quick-start</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Para Empezar con Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/starters">gatsby.dev/starters</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Guía de Referencia Rápida</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/recipes">gatsby.dev/recipes</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Agregar Imágenes</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/image">gatsby.dev/image</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>APIs de Gatsby Node</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/api">gatsby.dev/api</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Querying con GraphQL</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/graphql">gatsby.dev/graphql</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Implementación y Alojamiento</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/deploy">gatsby.dev/deploy</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Usando Gatsby Link</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/link">gatsby.dev/link</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Static Query</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/static-query">gatsby.dev/static-query</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Cómo Contribuir</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/contribute">gatsby.dev/contribute</a></p>
                </td>
            </tr>
        </tbody>
    </table>
    <p><a href="https://www.gatsbyjs.org/">gatsbyjs.org</a></p>
    <p><a href="https://twitter.com/gatsbyjs">twitter.com/gatsbyjs</a></p>
    <h2>Comandos de Gatsby CLI</h2>
    <p>Primero, instala el ejecutable global:
        <br />
        <code>npm install -g gatsby-cli</code></p>
    <p>Ejecuta <code>gatsby --help</code> para obtener una lista de comandos y opciones.</p>
    <h3><code>gatsby new <span style="font-weight:normal">nombre-de-mi-sitio</span></code></h3>
    <p>Crea un nuevo sitio local Gatsby con el iniciador predeterminado (ve "Comandos de inicio rápido" en esta hoja de trucos sobre cómo usar otros iniciadores).</p>
    <h3><code>gatsby develop</code></h3>
    <p>Inicia el servidor de desarrollo Gatsby.</p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>-H, --host</code></p>
                </td>
                <td>
                    <p>Establece el host. Por defecto es <code>localhost</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-p, --port</code></p>
                </td>
                <td>
                    <p>Establece el puerto. Por defecto env.PORT o <code>8000</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-o, --open</code></p>
                </td>
                <td>
                    <p>Abre el sitio en tu navegador predeterminado</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-S, --https</code></p>
                </td>
                <td>
                    <p>Usa HTTPS</p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>gatsby build</code></h3>
    <p>Compila tu aplicación y prepárela para su implementación.<br /></p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>--prefix-paths</code></p>
                </td>
                <td>
                    <p>Crear sitio con rutas de enlace con prefijo<br />(especifica un <code>pathPrefix</code> en tu config)</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>--no-uglify</code></p>
                </td>
                <td>
                    <p>Compila el sitio sin uglificar los paquetes JS <br />(para depurar)</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>--open-tracing-config-file</code></p>
                </td>
                <td>
                    <p>Archivo de configuración del trazador (compatible con OpenTracing). Ver <a href="https://gatsby.dev/tracing">gatsby.dev/tracing</a></p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>gatsby serve</code></h3>
    <p>Sirve la compilación de producción para pruebas.</p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>-H, --host</code></p>
                </td>
                <td>
                    <p>Establece el host. Por defecto es <code>localhost</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-p, --port</code></p>
                </td>
                <td>
                    <p>Establece el puerto. Por defecto es <code>9000</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-o, --open</code></p>
                </td>
                <td>
                    <p>Abre el sitio en tu navegador predeterminado</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>--prefix-paths</code></p>
                </td>
                <td>
                    <p>Crear sitio con rutas de enlace con prefijo (si usas <code>pathPrefix</code> en tu <code>gatsby-config.js</code>)</p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>gatsby info</code></h3>
    <p>Obtén información útil del entorno que será necesaria al informar un error en <a href="https://github.com/gatsbyjs/gatsby/issues">github.com/gatsbyjs/gatsby/issues</a>.</p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>-C, --clipboard</code></p>
                </td>
                <td>
                    <p>Copia automáticamente la información del entorno al portapapeles</p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>gatsby clean</code></h3>
    <p>Limpia los derectorios <code>.cache</code> y <code>public</code> de Gatsby.</p>
    <h2>¡Camisetas, gorras, sudaderas y más!</h2>
    <p>¡Suscríbete al newsletter de Gatsby y <strong>obtén un 30% de descuento</strong> en tu compra en la tienda Gatsby! (<a href="https://gatsby.dev/store">gatsby.dev/store</a>)</p>
    <p>Suscríbete en <a href="https://gatsby.dev/discount">gatsby.dev/discount</a></p>
    <h2>Comandos de Inicio Rápido</h2>
    <p>Crea un nuevo sitio de Gatsby con el iniciador "Blog":<br />
    <code>gatsby new mi-nuevo-blog https://github.com/gatsbyjs/gatsby-starter-blog</code></p>
    <p>Ve al directorio de tu nuevo sitio e inícialo:<br />
    <code>cd mi-nuevo-blog/<br />
    gatsby develop</code></p>
    <p>Tu sitio ahora se está ejecutando en <code>http://localhost:8000</code>!</p>
    <p>También verás un segundo link: <code>http://localhost:8000/___graphql</code>. Esta es una herramienta que puedes usar para experimentar con la consulta de tus datos. Obtén más información al respecto en <a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a></p>
    <p>Para más iniciadores Gatsby, visita <a href="https://gatsby.dev/starters">gatsby.dev/starters</a>.</p>
    <h2>Definiciones de Archivos</h2>
    <p>Cada uno de estos archivos debe estar localizado en la raíz de tu carpeta de proyecto Gatsby. Ve <a href="https://gatsby.dev/projects">gatsby.dev/projects</a></p>
    <p><code>gatsby-config.js</code> — configura opciones para tu sitio Gatsby, con metadatos para el título del proyecto, descripción, plugins, etc.</p>
    <p><code>gatsby-node.js</code> — implementa las API de Gatsby Node.js para personalizar y ampliar la configuración predeterminada que afecta el proceso de compilación</p>
    <p><code>gatsby-browser.js</code> — personaliza y amplia la configuración predeterminada que afecta al navegador, utilizando las API del navegador de Gatsby</p>
    <p><code>gatsby-ssr.js</code> — usa las API de server-side rendering de Gatsby para personalizar la configuración predeterminada que afecta el server-side rendering</p>
=======
  <h2>Page 1</h2>
  <a
    href="/cheat-sheet_page_1.png"
    title="Click to open image in a new window"
    target="_blank"
    style="display:block;"
  >
    <img
      src="/cheat-sheet_page_1.png"
      alt="Cheat Sheet - page 1"
      style="display:block; margin:0;"
    />
  </a>
  <h2>Page 2</h2>
  <a
    href="/cheat-sheet_page_2.png"
    title="Click to open image in a new window"
    target="_blank"
    style="display:block;"
  >
    <img
      src="/cheat-sheet_page_2.png"
      alt="Cheat Sheet - page 2"
      style="display:block; margin:0;"
    />
  </a>
</figure>
<div
  id="cheat_sheet-text"
  style=" position: absolute; height: 1px; width: 1px;overflow: hidden; clip: rect(1px, 1px, 1px, 1px);"
>
  <h2>Gatsby Cheat Sheet contents</h2>
  <p>
    v1.0 for Gatsby 2.x
    <a href="https://gatsby.dev/cheatsheet">
      Latest version <span aria-hidden="true">↗</span>
    </a>
  </p>
  <h2>Top Docs</h2>
  <table>
    <tbody>
      <tr>
        <td>
          <p>Gatsby Docs</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/docs">gatsby.dev/docs</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Gatsby on GitHub</p>
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
          <p>Gatsby Tutorial</p>
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
            Quick Start
            <br />
            (for intermediate and advanced developers)
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
          <p>Gatsby Starters</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/starters">gatsby.dev/starters</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Quick Reference Guide</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/recipes">gatsby.dev/recipes</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Adding Images</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/image">gatsby.dev/image</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Gatsby Node APIs</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/api">gatsby.dev/api</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Querying with GraphQL</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/graphql">gatsby.dev/graphql</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Deploying and Hosting</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/deploy">gatsby.dev/deploy</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Using Gatsby Link</p>
        </td>
        <td>
          <p>
            <a href="https://gatsby.dev/link">gatsby.dev/link</a>
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Static Query</p>
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
          <p>How to Contribute</p>
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
  <h2>Gatsby CLI Commands</h2>
  <p>
    First, install the global executable:
    <br />
    <code>npm install -g gatsby-cli</code>
  </p>
  <p>
    Run <code>gatsby --help</code> for a list of commands and options.
  </p>
  <h3>
    <code>
      gatsby new <span style="font-weight:normal">my-site-name</span>
    </code>
  </h3>
  <p>
    Create a new local Gatsby site using the default starter (see “Quick Start
    Commands” in this cheat sheet on how to use other starters).
  </p>
  <h3>
    <code>gatsby develop</code>
  </h3>
  <p>Start the Gatsby development server.</p>
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
            Set host. Defaults to <code>localhost</code>
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
            Set port. Defaults to env.PORT or <code>8000</code>
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
          <p>Open the site in your (default) browser for you</p>
        </td>
      </tr>
      <tr>
        <td>
          <p>
            <code>-S, --https</code>
          </p>
        </td>
        <td>
          <p>Use HTTPS</p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>
    <code>gatsby build</code>
  </h3>
  <p>
    Compile your application and make it ready for deployment.
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
            Build site with link paths prefixed
            <br />
            (set <code>pathPrefix</code> in your config)
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
            Build site without uglifying JS bundles
            <br />
            (for debugging)
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
            Tracer configuration file (OpenTracing compatible). See{" "}
            <a href="https://gatsby.dev/tracing">gatsby.dev/tracing</a>
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>
    <code>gatsby serve</code>
  </h3>
  <p>Serve the production build for testing.</p>
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
            Set host. Defaults to <code>localhost</code>
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
            Set port. Defaults to <code>9000</code>
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
          <p>Open the site in your (default) browser for you</p>
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
            Serve site with link paths prefixed (if built with{" "}
            <code>pathPrefix</code> in your <code>gatsby-config.js</code>)
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>
    <code>gatsby info</code>
  </h3>
  <p>
    Get helpful environment information which will be required when reporting a
    bug at{" "}
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
          <p>Automagically copy environment information to clipboard</p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>gatsby clean</h3>
  <p>
    Wipe out Gatsby’s <code>.cache</code> and <code>public</code> directories.
  </p>
  <h2>T-Shirts, Hats, Hoodies, and more!</h2>
  <p>
    Sign up for the Gatsby Newsletter and <strong>get 30% off</strong> your
    Gatsby Store purchase! (
    <a href="https://gatsby.dev/store">gatsby.dev/store</a>)
  </p>
  <p>
    Sign up at <a href="https://gatsby.dev/discount">gatsby.dev/discount</a>
  </p>
  <h2>Quick Start Commands</h2>
  <p>
    Create a new Gatsby site using the “Blog” starter:
    <br />
    <code>
      gatsby new my-blog-starter https://github.com/gatsbyjs/gatsby-starter-blog
    </code>
  </p>
  <p>
    Navigate into your new site’s directory and start it up:
    <br />
    <code>
      cd my-blog-starter/
      <br />
      gatsby develop
    </code>
  </p>
  <p>
    Your site is now running at <code>http://localhost:8000</code>!
  </p>
  <p>
    {/* prettier-ignore */}
    You’ll also see a second link: <code>http://localhost:8000/___graphql</code>.
    This is a tool you can use to experiment with querying your data. Learn more
    about it at <a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a>
  </p>
  <p>
    For more Gatsby starters, visit{" "}
    <a href="https://gatsby.dev/starters">gatsby.dev/starters</a>.
  </p>
  <h2>Helpful File Definitions</h2>
  <p>
    Each of these files should live at the root of your Gatsby project folder.
    See <a href="https://gatsby.dev/projects">gatsby.dev/projects</a>
  </p>
  <p>
    <code>gatsby-config.js</code> — configure options for a Gatsby site, with
    metadata for project title, description, plugins, etc.
  </p>
  <p>
    <code>gatsby-node.js</code> — implement Gatsby’s Node.js APIs to customize
    and extend default settings affecting the build process
  </p>
  <p>
    <code>gatsby-browser.js</code> — customize and extend default settings
    affecting the browser, using Gatsby’s browser APIs
  </p>
  <p>
    <code>gatsby-ssr.js</code> — use Gatsby’s server-side rendering APIs to
    customize default settings affecting server-side rendering
  </p>
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097
</div>
