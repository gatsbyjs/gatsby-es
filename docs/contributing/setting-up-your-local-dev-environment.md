---
title: Configuración de tu entorno de desarrollo local
---

Esta página describe cómo configurar para que contribuyas al core de Gatsby y su ecosistema. Para obtener instrucciones sobre cómo trabajar con la documentación, visita la página [contribuciones a la documentación](/contributing/docs-contributions/). Para instrucciones de configuración del blog y sitio web, visita la página [blog y contribuciones al sitio web](/contributing/blog-and-website-contributions/).

> Gatsby usa un patrón de "monorepo" para manejar sus dependencias y confía en
> [Lerna](https://lerna.js.org/) y en [Yarn](https://yarnpkg.com/en/) para configurar el repositorio para cambios tanto de desarrollo como en la documentación de la infraestructura.

## Usando Yarn

Yarn es un gestor de paquetes para tu código, similar a [NPM](https://www.npmjs.com/). Mientras que NPM se utiliza para desarrollar sitios Gatsby con el CLI, contribuir al repositorio de Gatsby requiere Yarn por la siguiente razón: utilizamos [workspaces](https://yarnpkg.com/lang/en/docs/workspaces/) de Yarn, característica que viene muy útil para monorepos. Nos permite instalar dependencias desde múltiples archivos `package.json` en subcarpetas, permitiendo un proceso de instalación más rápido y ligero.

```json:title=package.json
{
  "workspaces": ["workspace-a", "workspace-b"]
}
```

## Instrucciones de instalación del repositorio de Gatsby

<<<<<<< HEAD
- Asegúrate de tener instalada la última versión **LTS** de Node (>= 10.16.0). `node --version`
- [Instala](https://yarnpkg.com/en/docs/install) el gestor de dependencias Yarn.
- Asegúrate que tienes la última versión de Yarn instalado (>= 1.0.2). `yarn --version`
- Haz fork del [repositorio oficial](https://github.com/gatsbyjs/gatsby).
- Clona tu fork: `git clone --depth=1 https://github.com/<your-username>/gatsby.git`
- Configura el repositorio e instala las dependencias: `yarn run bootstrap`
- Asegúrate que tus pruebas pasan: `yarn test`
- Crea una branch topics: `git checkout -b topics/new-feature-name`
- Consulta la [documentación de las instrucciones de configuración](/contributing/docs-contributions#docs-site-setup-instructions) a continuación solo para cambios de documentación.
- Ejecuta `yarn run watch` desde la raíz del repositorio para ver si hay cambios en el código fuente de los paquetes y compilar estos cambios sobre la marcha mientras trabajas.
  - Ten en cuenta que el comando watch puede ser intensivo en recursos. Para limitarlo a los paquetes en los que estás trabajando, agrega un indicador de alcance, como `yarn run watch --scope={gatsby,gatsby-cli}`.
  - Para ver los cambios de sólo un paquete, ejecuta `yarn run watch --scope=gatsby`.
- Instala [gatsby-dev-cli](https://www.npmjs.com/package/gatsby-dev-cli) globalmente: `yarn global add gatsby-dev-cli`
- Ejecuta `yarn install` en cada uno de los sitios que estás probando.
- Para cada uno de tus sitios de prueba de Gatsby, ejecuta el comando `gatsby-dev` dentro del directorio del sitio de prueba para copiar
  los archivos construidos desde tu copia clonada de Gatsby. Observarás tus cambios
  a los paquetes de Gatsby y copiarlos en el sitio. Para instrucciones más detalladas
  mira el [README de gatsby-dev-cli](https://www.npmjs.com/package/gatsby-dev-cli) y échale un vistazo al [video de la demo del gatsby-dev-cli](https://www.youtube.com/watch?v=D0SwX1MSuas).
  - Nota: si planeas modificar directamente los paquetes que se exportan desde `gatsby`, debes añadirlos manualmente a tus sitios de prueba para que figuren en el `package.json` (p.ej. `yarn add gatsby-link`), o especificarlos explícitamente con `gatsby-dev --packages gatsby-link`).
- Añade tests y código para tus cambios.
- Una vez que haya terminado, asegúrate de que todas las pruebas todavía pasan: `yarn test`.
  - Para ejecutar pruebas para un solo paquete puedes ejecutar: `yarn jest <package-name>`.
  - Para ejecutar un único fichero de prueba puedes ejecutar: `yarn jest <file-path>`.
- Commit y push a tu fork.
- Crea un pull request desde tu branch.
=======
### Install Node and Yarn

- Ensure you have the latest **LTS** version of Node installed (>= 10.16.0). `node --version`
- [Install](https://yarnpkg.com/en/docs/install) the Yarn package manager.
- Ensure you have the latest version of Yarn installed (>= 1.0.2). `yarn --version`

### Fork, clone, and branch the repository

- [Fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) the [official `gatsbyjs/gatsby` repository](https://github.com/gatsbyjs/gatsby).
- Clone your fork: `git clone --depth=1 https://github.com/<your-username>/gatsby.git`
- Set up repo and install dependencies: `yarn run bootstrap`
- Make sure tests are passing for you: `yarn test`
- Create a topic branch: `git checkout -b topics/new-feature-name`

### Docs only changes

- See [docs setup instructions](/contributing/docs-contributions#docs-site-setup-instructions) for docs-only changes.
- Run `yarn run watch` from the root of the repo to watch for changes to packages' source code and compile these changes on-the-fly as you work.

  - Note that the watch command can be resource intensive. To limit it to the packages you're working on, add a scope flag, like `yarn run watch --scope={gatsby,gatsby-cli}`.
  - To watch just one package, run `yarn run watch --scope=gatsby`.

### Gatsby functional changes

- Install [gatsby-cli](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli):
  - Make sure you have the Gatsby CLI installed with `gatsby -v`,
  - if not, install globally: `yarn global add gatsby-cli`
- Install [gatsby-dev-cli](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-dev-cli):
  - Make sure you have the Gatsby Dev CLI installed with `gatsby-dev -v`
  - if not, install globally: `yarn global add gatsby-dev-cli`
- Run `yarn install` in each of the sites you're testing.
- For each of your Gatsby test sites, run the `gatsby-dev` command inside the test site's directory to copy
  the built files from your cloned copy of Gatsby. It'll watch for your changes
  to Gatsby packages and copy them into the site. For more detailed instructions
  see the [gatsby-dev-cli README](https://www.npmjs.com/package/gatsby-dev-cli) and check out the [gatsby-dev-cli demo video](https://www.youtube.com/watch?v=D0SwX1MSuas).

  - Note: if you plan to modify packages that are exported from `gatsby` directly, you need to either add those manually to your test sites so that they are listed in `package.json` (e.g. `yarn add gatsby-link`), or specify them explicitly with `gatsby-dev --packages gatsby-link`).

### Add tests

- Add tests and code for your changes.
- Once you're done, make sure all tests still pass: `yarn test`.

  - To run tests for a single package you can run: `yarn jest <package-name>`.
  - To run a single test file you can run: `yarn jest <file-path>`.

### Commits and pull requests

- Commit and push to your fork.
- Create a pull request from your branch.

### Sync your fork

- GitHub Help Page [Syncing a fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
- GitHub Help Page [Merging an upstream repository into your fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/merging-an-upstream-repository-into-your-fork)
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc
