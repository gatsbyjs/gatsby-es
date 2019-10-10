---
title: Como abrir un Pull Request
---

Una gran parte de contribuir a código abierto es enviar cambios a un proyecto: mejoras al código fuente o pruebas, actualizaciones a contenido de documentos, inclusive errores tipográficos o hipervínculos rotos. Este documento cubrirá lo que necesitas saber para **abrir un pull request** en Gatsby.

## ¿Qué es un Pull Request (PR)?

En caso de que no estés familiarizado, aquí está como el equipo de GitHub [define un pull request](https://help.github.com/en/articles/about-pull-requests):

> Los Pull requests te permiten decir a otros acerca de cambios que has subido en una rama de un repositorio en GitHub. Una vez que un pull request es abierto, puedes discutir y revisar los cambios potenciales con colaboradores y agregar commits de seguimiento antes de que tus cambios sean incluidos en la rama de master (o base).

Gatsby utiliza el proceso de PR para revisar y probar cambios antes que sean agregados al repositorio de GitHub de Gatsby. Cualquier persona puede abrir un pull request. El mismo proceso es utilizado por todos los contribuidores, sea que ésta sea tu primera contribución a código abierto (open source) o que seas un miembro del equipo principal de Gatsby.

Cuando alguien quiere contribuir a Gatsby, abren una solicitud para _hacer un pull request_ (extraer) de su código hacia dentro del repositorio. Dependiendo del tipo de cambio hecho, los PRs son categorizados como de:

- [Documentación](#documentation)
- [Código](#code-changes)
- [Starters o Galería de sitios](#starters-or-site-showcase)
- [Entradas de Blog](#blog-posts)

Recomendaciones para diferentes tipos de contribuciones se encontrarán en esta guía asi como a través de los documentos de contribuciones.

## Cosas a saber antes de abrir un PR

Típicamente recomendamos [abrir un issue](/contributing/how-to-file-an-issue/) antes de un pull request si no hay ya un issue para el problema que quieres solucionar. Esto ayuda a facilitar una discusión antes de decidir una implementación.

Para algunos cambios, como errores tipográficos o hipervínculos rotos, sería apropiado abrir un pequeño PR por si mismo. Esto es de algún modo subjetivo de modo que si tienes preguntas, [siéntete libre de consultarnos](/contributing/how-to-contribute/#not-sure-how-to-start-contributing).

El equipo principal de Gatsby usa un proceso de "triaging" delineado en [Manejando los Pull Requests](/contributing/managing-pull-requests/), si estás interesado en aprender más acerca de como funciona eso.

## Abriendo PRs en Gatsby

Para cualquier tipo de cambio a archivos en el repo de Gatsby, puedes seguir los siguientes pasos. Asegúrate de comprobar las recomendaciones adicionales para contribuir a varias partes del repo más adelante en este documento, como de cambios de documentos, entradas de blog, starters o mejoras en código y pruebas.

Algunos PRs pueden ser realizados completamente desde la [interfaz de usuario de GitHub](https://help.github.com/en/articles/creating-a-pull-request), tal como ediciones a los archivos README o documentos.

Para probar cambios localmente frente al [sitio y archivos de proyecto de Gatsby](https://github.com/gatsbyjs/gatsby), puedes hacer un fork del repositorio e instalar partes de él para que corran en tu computadora localmente.

- [Hacer un fork y clonar el repositorio de Gatsby](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions).
- Instalar [yarn](https://yarnpkg.com/) para instalar las dependencias y compilar el proyecto.
- Sigue las instrucciones para la parte del proyecto que deseas cambiar. (Ver secciones específicas abajo.)
- [Crear una rama en Git](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) para aislar tus cambios:

  ```shell
  git checkout -b some-change
  ```

- Una vez que tienes cambios en Git que quieres subir, [agrégalos y crea un commit](https://help.github.com/en/articles/adding-a-file-to-a-repository-using-the-command-line). Para información sobre como estructurar tus commits, revisa la guía de [Manejando PRs](/contributing/managing-pull-requests/#commit-and-pr-title).
  - Usando un carácter de punto `.` agregará todos los archivos no seguidos todavía en el actual directorio y subdirectorios.
  ```shell
  git add .
  ```
  - Usando una herramienta visual como [GitHub Desktop](https://desktop.github.com/) o [GitX](https://rowanj.github.io/gitx/) puede ayudar para elegir sobre qué archivos y lineas hacer un commit.
- Haciendo commit del código hará correr el linter automático que usa [Prettier](https://prettier.io). Para ejecutar el linter manualmente, ejecuta un script npm en el directorio base del proyecto:
  ```shell
  npm run format
  ```
- Haz commit de todos los cambios del "linting" antes de subir cambios [enmendando el commit previo](https://help.github.com/en/articles/changing-a-commit-message) o agregando un nuevo commit. Para más acerca de "linting" y pruebas, visita la guía de [Manejando PRs](/contributing/managing-pull-requests/#automated-checks).
  ```shell
  git commit --amend
  ```
- Sube tus cambios a tu fork, asumiendo que está configurado como [`origin`](https://www.git-tower.com/learn/git/glossary/origin):
  ```shell
  git push origin head
  ```
- Para abrir un PR con tus cambios ante el repo de Gatsby, puedes usar la [interfaz de usuario de Pull Requests de GitHub](https://help.github.com/en/articles/creating-a-pull-request). Alternativamente, puedes usar la linea de comandos: recomendamos [hub](https://github.com/github/hub) para ello.

### PRs de Documentación

El sitio de documentación de Gatsby.js vive mayormente en los directorios [www](https://github.com/gatsbyjs/gatsby/tree/master/www) y [docs](https://github.com/gatsbyjs/gatsby/tree/master/docs) en GitHub, incluyendo documentaciones y contenido de tutoriales. Hay también algunos [ejemplos en el repositorio de Gatsby](https://github.com/gatsbyjs/gatsby/tree/master/examples) referenciados en la documentación.

Pasos adicionales para PRs de docs:

- Para cambios solamente de documentación, considera usar `git checkout -b docs/some-change` o `git checkout -b docs-some-change`, ya que esto recortará el proceso de CI (o integración continua) y solo ejecutará tareas de "linting".

Más instrucciones pueden ser encontradas en la página de [contribuciones a documentación](/contributing/docs-contributions/).

### Cambios de código

Instrucciones para realizar cambios al código fuente de Gatsby, pruebas, materiales internos, APIs, paquetes, y más pueden ser encontrados en la documentación de contribuciones en [estableciendo tu ambiente de desarrollo local](/contributing/setting-up-your-local-dev-environment/). Hay también detalles adicionales en la página de [Contribuciones de código](/contributing/code-contributions/).

### Starters o Galería de sitios

Hay páginas específicas acerca de cómo contribuir a varias partes del ecosistema Gatsby: :

- [Aplicaciones a la galería](/contributing/site-showcase-submissions/)
- [Librería de Starters](/contributing/submit-to-starter-library/)

### Entradas del Blog

Para contribuir al blog de Gatsby, es necesario primero pasar tu idea de contenido por el equipo de Gatsby antes de enviarla. Para más información, refiérete a la página de [contribuciones al blog y sitio web](/contributing/blog-and-website-contributions/), incluyendo cómo proponer una idea y cómo configurar el blog para que se ejecute localmente.

## Actualiza tu fork con los últimos cambios de Gatsby

El repo de Gatsby de Github es muy activo, así que es probable que necesites actualizar tu fork con los últimos cambios para hacer un merge de tu código. Esto requiere agregar a Gatsby como un [upstream remote](https://help.github.com/en/articles/configuring-a-remote-for-a-fork):

- Establece la URL del repositorio de Gatsby como una fuente remota. El nombre de la fuente remota es arbitrario; este ejemplo usa `upstream`.
  ```shell
  git remote set-url upstream git@github.com:gatsbyjs/gatsby.git
  ```
  - _Nota: esta sintaxis [usa SSH y llaves de seguridad: también puedes usar `https`](https://help.github.com/en/articles/which-remote-url-should-i-use) con tu usuario/contraseña._
- Puedes verificar el nombre del remoto y URL en cualquier momento:
  ```shell
  git remote -v
  ```
- Traer los últimos cambios desde Gatsby:
  ```shell
  git fetch upstream master
  ```
- [En la rama](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) que quieres actualizar, haz un merge de cualquier cambio desde Gatsby hacia tu fork:
  ```shell
  git merge upstream master
  ```
  - Si hay [conflictos de merge](https://help.github.com/en/articles/resolving-a-merge-conflict-on-github), querrás encargarte de ellos para conseguir un merge limpio.
- Una vez que tu rama está en estado funcional, sube los cambios a tu fork:
  ```shell
  git push origin head
  ```

Para más información sobre cómo trabajar con repositorios upstream, [visita la documentación de GitHub](https://help.github.com/en/articles/configuring-a-remote-for-a-fork).

_**Nota:** como miembro del repositorio de Gatsby, también puedes clonarlo directamente en vez de hacer un fork, y subir tus cambios a [ramas de funcionalidades](https://git-scm.com/book/en/v1/Git-Branching-Branching-Workflows)._

## Recursos adicionales

- CSS Tricks: [Cómo contribuir a un proyecto open source](https://css-tricks.com/how-to-contribute-to-an-open-source-project/)
- [Creando un pull request](https://help.github.com/en/articles/creating-a-pull-request) de GitHub
- [Configurando un remoto para un fork](https://help.github.com/en/articles/configuring-a-remote-for-a-fork)
- [¿Qué remoto debería usar?](https://help.github.com/en/articles/which-remote-url-should-i-use)
- [Merge y ramas de Git](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
- [Ramas por funcionalidad y flujos de trabajo](https://git-scm.com/book/en/v1/Git-Branching-Branching-Workflows)
- [Resolviendo conflictos de merge](https://help.github.com/en/articles/resolving-a-merge-conflict-on-github)
- [Manejando Pull Requests](/contributing/managing-pull-requests/) del equipo principal de Gatsby.
