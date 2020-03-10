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
</div>
