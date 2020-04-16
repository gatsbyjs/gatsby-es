---
title: Configuración de tu entorno de desarrollo local
---

Esta página describe cómo configurar para que contribuyas al core de Gatsby y su ecosistema. Para obtener instrucciones sobre cómo trabajar con la documentación, visita la página [contribuciones a la documentación](/contributing/docs-contributions/). Para instrucciones de configuración del sitio web, visita la página [contribuciones al sitio web](/contributing/website-contributions/).

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

### Instalar Node y Yarn

- Asegúrate de tener instalada la última versión **LTS** de Node (>= 10.16.0). `node --version`
- [Instala](https://yarnpkg.com/en/docs/install) el gestor de dependencias Yarn.
- Asegúrate que tienes la última versión de Yarn instalado (>= 1.0.2). `yarn --version`

### Fork, clonar y hacer un branch del repositorio

- Haz fork del [repositorio oficial](https://github.com/gatsbyjs/gatsby).
- Clona tu fork: `git clone --depth=1 https://github.com/<your-username>/gatsby.git`
- Configura el repositorio e instala las dependencias: `yarn run bootstrap`
- Asegúrate que tus pruebas pasan: `yarn test`
- Crea una branch topics: `git checkout -b topics/new-feature-name`

### Cambios solo a documentación

- Consulta la [documentación de las instrucciones de configuración](/contributing/docs-contributions#docs-site-setup-instructions) a continuación solo para cambios de documentación.
- Ejecuta `yarn run watch` desde la raíz del repositorio para ver si hay cambios en el código fuente de los paquetes y compilar estos cambios sobre la marcha mientras trabajas.
  - Ten en cuenta que el comando watch puede ser intensivo en recursos. Para limitarlo a los paquetes en los que estás trabajando, agrega un indicador de alcance, como `yarn run watch --scope={gatsby,gatsby-cli}`.
  - Para ver los cambios de sólo un paquete, ejecuta `yarn run watch --scope=gatsby`.

### Cambios funcionales a Gatsby

- Instala [gatsby-cli](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli):
  - Asegúrate de tener instalado el CLI de Gatsby con `gatsby -v`,
  - Sí no, instalalo globalmente: `yarn global add gatsby-cli`
- Instala [gatsby-dev-cli](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-dev-cli):
  - Asegúrate de tener instalado el CLI de desarrollo de Gatsby con `gatsby-dev -v`,
  - Sí no, instalalo globalmente: `yarn global add gatsby-dev-cli`
- Ejecuta `yarn install` en cada uno de los sitios que estás probando.
- Para cada uno de tus sitios de prueba de Gatsby, ejecuta el comando `gatsby-dev` dentro del directorio del sitio de prueba para copiar
  los archivos construidos desde tu copia clonada de Gatsby. Observará tus cambios
  a los paquetes de Gatsby y los copiará en tu sitio. Para instrucciones más detalladas
  mira el [README de gatsby-dev-cli](https://www.npmjs.com/package/gatsby-dev-cli) y échale un vistazo al [video de la demo del gatsby-dev-cli](https://www.youtube.com/watch?v=D0SwX1MSuas).
  - Nota: si planeas modificar directamente los paquetes que se exportan desde `gatsby`, debes añadirlos manualmente a tus sitios de prueba para que figuren en el `package.json` (p.ej. `yarn add gatsby-link`), o especificarlos explícitamente con `gatsby-dev --packages gatsby-link`).

### Añadir pruebas

- Añade pruebas y código para tus cambios.
- Una vez que hayas terminado, asegúrate de que todas las pruebas todavía pasan: `yarn test`.

  - Para ejecutar pruebas para un solo paquete puedes ejecutar: `yarn jest <package-name>`.
  - Para ejecutar un único fichero de prueba puedes ejecutar: `yarn jest <file-path>`.

### Commits y pull requests

- Commit y push a tu fork.
- Crea un pull request desde tu branch.

### Sincronizar tu fork

- Página de ayuda de GitHub: [Sincronizando un fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
- Página de ayuda de  GitHub: [Haciendo merge de un repositorio "upstream" a tu fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/merging-an-upstream-repository-into-your-fork)
