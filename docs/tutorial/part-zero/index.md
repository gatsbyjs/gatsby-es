---
title: Configura tu Entorno de Desarrollo
typora-copy-images-to: ./
disableTableOfContents: true
---

Antes de comenzar a crear tu primer sitio Gatsby, debes familiarizarte con algunas tecnologías web básicas y asegurarte de haber instalado todas las herramientas de software necesarias.

## Familiarízate con la línea de comandos

La línea de comandos es una interface de texto para ejecutar comandos en tu ordenador. Muchas veces nos referimos a ella como la terminal. En este tutorial lo llamaremos de ambas formas. Es muy parecido a usar el Finder en Mac o el Explorador en Windows. Finder y Explorer son ejemplos de Interfaz gráfica de usuario (GUI). La línea de comandos es una manera poderosa, basada en texto, para interactuar con tu ordenador.

Toma un momento y abre la interfaz de línea de comandos (CLI) de tu computadora. Dependiendo de que sistema operativo estés utilizando, mira las [**instrucciones para Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instrucciones para Windows**](https://www.lifewire.com/how-to-open-command-prompt-2618089) o las [**instrucciones para Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

_**Nota:** Sí eres nuevo con la línea de comandos, "ejecutar" un comando, significa "escribir una serie de instrucciones en el símbolo del sistema, y oprimir la tecla Enter". Los comandos serán mostrados en una caja destacada, algo como `node --version`, pero no toda caja destacada es un comando! Sí algo es un comando será mencionado como algo que tienes que correr/ejecutar_

## Instala Node.js para tu sistema operativo

Node.js es un ambiente que puede ejecutar código Javascript fuera del navegador web. Gatsby esta construído con Node.js. Para ponerte en marcha con Gatsby, necesitarás tener una versión reciente instalada en tu computadora. npm viene junto a Node.js así que sí no tienes npm, probablemente tampoco tienes Node.js.

### Instrucciones para Mac

Para instalar Gatsby y Node.js en una Mac, es recomendado usar [Homebrew](https://brew.sh/). Un poco de configuración al inicio puede evitarte algunos dolores de cabeza despues!

#### Cómo instalar o verificar que tienes instalado Homebrew en tu computadora:

1. Abre tu Terminal.
2. Comprueba sí Homebrew está instalado ejecutando `brew -v`. Deberías ver "Homebrew" y un número de versión.

```shell
brew -v
```

3. Sí no, descarga e instala [Homebrew con estas instrucciones](https://docs.brew.sh/Installation).
4. Una vez que ya tienes instalado Homebrew, repite el paso 2 para verificar.

#### Instala las herramientas de línea de comandos de Xcode:

1. Abre tu Terminal.
2. Instala las herramientas de línea de comandos de Xcode ejecutando:

```shell
xcode-select --install
```

> 💡 Si el comando falla, descargalas [directamente del sitio de Apple](https://developer.apple.com/download/more/), después de iniciar sesión con una cuenta de desarrollador.

3. Después de empezar la instalación, serás llevado de nuevo a aceptar la licensia de software para las herramientas que vas a descargar.

#### Instala Node

1. Abre tu Terminal.
2. Instala node con Homebrew:

```shell
brew install node
```

> 💡 Si no quieres instalarlo mediante Homebrew, descarga la ultima versión de Node.js desde el [sitio oficial de Node.js](https://nodejs.org/en/), haz doble click en el archivo descargado y sigue el proceso de instalación.

### Instrucciones para Windows

- Descarga e instala la última versión de Node.js desde [el sitio oficial de Node.js](https://nodejs.org/es/)

### Instrucciones para Linux

Instala nvm (Gestor de versiones de Node) y las dependencias necesarias. nvm es usado para gestionar Node.js y todas sus versiones asociadas.

> 💡 Sí cuando instalas un paquete, te pide confirmación, teclea `y` y presiona enter._

Selecciona la distro:

- [Ubuntu, Debian, y otras distros basadas en apt](#ubuntu-debian-and-other-apt-based-distros)
- [Arch, Manjaro y otras distros basadas en pacman](#arch-manjaro-and-other-pacman-based-distros)
- [Fedora, RedHat, y otras distros basadas en dnf](#fedora-redhat-and-other-dnf-based-distros)

> 💡 Si la distribución de Linux que estas usando no aparece en la lista de aquí, por favor encuentra las instrucciones en la web.

#### Ubuntu, Debian, y otras distros basadas en `apt`:

1. Asegurate de que tu distribución de Linux esta lista para ejecutar actualizaciones:

```shell
sudo apt update
sudo apt -y upgrade
```

2. Instala `curl` que te permite transferir datos y descargar dependencias adicionales:

```shell
sudo apt-get install curl
```

3. Después de que termines de instalar todo, descarga la última versión de nvm:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

4. Confirma que ha funcionado. La salido del comando debe ser el número de versión:

```shell
nvm --version
```

5. Continua con la sección: [Configura la versión por defecto de Node.js](#set-default-nodejs-version)

#### Arch, Manjaro y otras distros basadas en `pacman`:

1. Asegurate de que tu distribucion esta lista:

```shell
sudo pacman -Sy
```

2. Estas distros vienen instaladas con `curl`, así que puedes utilizarlo para descargar nvm:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

3. Antes de utilizar nvm, necesitas instalar unas dependencias adicionales ejecutando:

```shell
sudo pacman -S grep awk tar
```

4. Confirma que ha funcionado. La salido del comando debe ser el número de versión:

```shell
nvm --version
```

5. Continua con la sección: [Configura la versión por defecto de Node.js](#set-default-nodejs-version)

#### Fedora, RedHat, y otras distros basadas en `dnf`:

1. Estas distros vienen instaladas con `curl`, así que puedes utilizarlo para descargar nvm:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

2. Confirma que ha funcionado. La salido del comando debe ser el número de versión:

```shell
nvm --version
```

3. Continua con la sección: [Configura la versión por defecto de Node.js](#set-default-nodejs-version)

#### Configura la versión por defecto de Node.js

Cuando nvm es instalado, no viene configurado con una versión en particular de Node por defecto. Tendrás que instalar la versión que deseas y configurar nvm para que la use. Este ejemplo usa la última versión lanzada de Node 10, pero números de versiones mas recientes pueden ser usados en su lugar.

```shell
nvm install 10
nvm use 10
```

Para confirmar que funcionó:

```shell
npm --version
node --version
```

La salida debería verse similar a la captura de pantalla de abajo, mostrando el número de versión en respuesta a los comandos.

![Verifica las versiones de Node.js y npm](01-node-npm-versions.png)

Una vez que hayas seguido los pasos de instalación y hayas comprobado que todo está instalado correctamente, puedes continuar con siguiente paso.

## Instala Git

Git es un software de control de versiones distribuido y de software libre diseñado para gestionar proyectos pequeños o grandes de una manera rápida y eficiente. Cuando instalas un "starter" de Gatsby, Gatsby usa Git internamente para descargar e instalar los ficheros requeridos para tu proyecto. Necesitarás Git instalado para configurar tu primer sitio web Gatsby.

Los pasos para descargar e instalar Git dependen de tu sistema operativo. Sigue los pasos para el tuyo:

- [Instala Git para macOS](https://filisantillan.com/como-instalar-git/#mac)
- [Instala Git para Windows](https://filisantillan.com/como-instalar-git/#windows)
- [Instala Git para Linux](https://filisantillan.com/como-instalar-git/#linux)

## Usando la Gatsby CLI

La línea de comandos de Gatsby (CLI) te permite crear rápidamente nuevos sitios web Gatsby y ejecutar comandos para el desarrollo de sitios web Gatsby. es un paquete npm público.

Gatsby CLI está disponible via npm y debe ser instalado de manera global en tu sistema con el comando:

```shell
npm install -g gatsby-cli
```

Para ver los comandos disponibles:

```shell
gatsby --help
```

![Echa un vistazo a los comandos disponibles con Gatsby](05-gatsby-help.png)

> 💡 Si no puedes ejecutar la Gatsby CLI por un problema de permisos, quizás te interese mirar [la documentación de npm para solucionar el problema de los permisos (inglés)](https://docs.npmjs.com/getting-started/fixing-npm-permissions), o [ésta guía (inglés)](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Crea un sitio web con Gatsby

Ahora ya estás listo para usar la línea de comandos de Gatsby (Gatsby CLI) para crear tu primer sitio web con Gatsby. Usándola, puedes descargar "plantillas" ("starters") (sitios parcialmente construidos con alguna configuración predeterminada) que te ayudarán a ir más rápido creando cierto tipo de sitios. La plantilla "Hello World" que usarás contiene los elementos básicos necesarios para un sitio web Gatsby.

1. Abre tu terminal
2. Crea un nuevo sitio mediante un starter:

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

> 💡 Que ha pasado?
>
> - `new` es un comando de Gatsby para crear un nuevo proyecto Gatsby.
> - Aquí, `hello-world` es un titulo arbitrario — puede ser cualquier cosa. La CLI pondrá el código de tu nuevo sitio web en una nueva carpeta con el nombre "hello-world".
> Por último, la URL de Github especificada apunta a un repositorio de código que almacena la plantilla (starter) que quieres utilizar.

> 💡 Dependiendo en la velocidad de descarga, la cantidad de tiempo que toma puede variar. Por razones de brevedad, el GIF de abajo fue pausado durante la parte de la instalación.

3. Cambiate hacia el directorio de trabajo.

```shell
cd hello-world
```

> 💡 Esto quiere decir 'Quiero cambiar de directorios (`cd`) al subdirectorio “hello-world”'. Cada vez que quieras ejecutar comandos en tu sitio web, necesitas estar en el contexto del sitio (en otras palabras, la terminal tiene que estar apuntando al directorio donde está el código).

4. Ejecuta el modo de desarrollo:

```shell
gatsby develop
```

> 💡 Éste comando inicia un servidor de desarrollo. Serás capaz de ver e interactuar con tu nuevo sitio web en un entorno de desarrollo — local (en tu ordenador, no publicado a internet).

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

### Mira tu sitio web en local

Abre una nueva pestaña en tu navegador y ve a `http://localhost:8000/`

![Página principal](04-home-page.png)

¡Felicidades! ¡Esto es el inicio de tu primer sitio hecho con Gatsby! 🎉

Puedes ver tu sitio web en local en `http://localhost:8000/` mientras tu servidor de desarrollo esté activo. Este es el proceso que has iniciado cuando ejecutaste el comando `gatsby develop`. Para detener el proceso (o cerrar el servidor de desarrollo), vuelve a la terminal, mantén presionada la tecla "control" y presiona la tecla "c" (ctrl-c). ¡Para iniciarlo nuevamente, ejecuta `gatsby develop` otra vez!

_**Nota:** Si estás en un entorno virtual (VM) como `vagrant` y/o te gustaría ejecutara el entorno de desarrollo desde tu dirección IP local, ejecuta `gatsby develop --host=0.0.0.0`. Ahora, el servidor de desarrollo escuchará tanto en `http://localhost` como tu dirección IP local._

## Configura un editor de código

Un editor de código es un programa diseñado específicamente para editar código. Hay opciones muy buenas disponibles.

### Descarga VS Code

La documentación de Gatsby a veces incluye capturas que fueron tomadas en VS Code, asi que si no tienes un editor de código preferido aún, usando VS Code te asegurarás que lo que ves en tu pantalla se verá como las capturas en el tutorial y la documentación. Si has escogido usar VS Code, visita el [sitio oficial de VS Code](https://code.visualstudio.com/#alt-downloads) y descarga la versión adecuada para tu sisstema operativo.

### Instala el plugin de Prettier

También recomendamos usar [Prettier](https://github.com/prettier/prettier), una herramienta que ayuda a formatear tu código y evitar errores.

Puedes usar Prettier directamente en tu editor de código usando el [plugin de Prettier para VS Code](https://github.com/prettier/prettier-vscode):

1. Abre la vista de las extensiones en VS Code (View => Extensions).
2. Busca "Prettier - Code formatter".
3. Presiona "Instalar". (Después de la instalación, te sugerirá reiniciar VS Code para habilitar la extensión. Nuevas versiones de VS Code habilitarán automáticamente la extensión después de descargarla.)

> 💡 Si no estás usando VS Code, visita la documentación de Prettier por [instructiones de instalación](https://prettier.io/docs/en/install.html) u [otras integraciones](https://prettier.io/docs/en/editors.html).

## ➡️ Qué sigue?

Resumiendo, en ésta sección tú:

- Aprendimos acerca de la línea de comandos y cómo usarla
- Instalamos y aprendimos Node.js y npm CLI, el sistema de control de versiones Git y Gatsby CLI
- Creamos un nuevo sitio web Gatsby usando la Gatsby CLI
- Ejecutamos el servidor de desarrollo Gatsby y visitamos tu sitio en local
- Descargamos un editor de código
- Instalamos un formateador de código llamado Prettier

Ahora, sigamos a [**conociendo los bloques de construcción de Gatsby**](/tutorial/part-one/).

## Referencias

### Descripción general de las tecnologías principales

No es necesario ser un experto en ésto ahora — ¡Si no lo eres, no te preocupes! Aprenderás mucho durante el transcurso de ésta serie de tutoriales. Estas son algunas de las tecnologías web más comunes y que usarás para crear sitios web Gatsby:

- **HTML**: Lenguaje de marcado que todo navegador web puede entender. Son las siglas en inglés de HyperText Markup Language. HTML le da al contenido web una estructura informativa universal, definiendo cosas como encabezados, párrafos y más.
- **CSS**: Un lenguaje de presentación utilizado para diseñar la apariencia de su contenido web (fuentes, colores, diseño, etc.). Son las siglas en inglés de Cascading Style Sheets.
- **JavaScript**: Un lenguaje de programación que nos ayuda a hacer que la web sea dinámica e interactiva.
- **React**: Una librería de código (creada con JavaScript) para construir interfaces de usuario. Es el framework que Gatsby usa para crear páginas y estructurar contenido.
- **GraphQL**: Un lenguaje de consulta que le permite extraer datos en su sitio web. Es la interfaz que Gatsby usa para gestionar los datos del sitio.

### Qué es un sitio web?

Para una introducción completa de lo que es un sitio web, --incluida una introducción a HTML y CSS--, mira "[**Building your first web page**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)". Es un gran sitio para comenzar a aprender sobre la web. Para una introducción más práctica a [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css) y [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), consulta los tutoriales de Codecademy. [**React**](https://es.reactjs.org/tutorial/tutorial.html) y [**GraphQL**](https://graphql.org/graphql-js/) también tienen sus propios tutoriales introductorios.

### Aprende más sobre la línea de comandos

Para una excelente introducción al uso de la línea de comandos, consulte el [**tutorial de la línea de comandos de Codecademy**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) para usuarios de Mac y Linux, y [**este tutorial**](https://www.computerhope.com/issues/chusedos.htm) para usuarios de Windows. Incluso si es un usuario de Windows, la primera página del tutorial de Codecademy es una lectura valiosa. Explica qué es la línea de comandos, no solo cómo interactuar con ella.

### Aprende más sobre npm

npm es un administrador de paquetes de JavaScript. Un paquete es un módulo de código que puedes elegir incluir en tus proyectos. Si acabas de descargar e instalar Node.js, ¡npm se instaló también!

npm tiene tres componentes distintos: el sitio web de npm, el registro de npm y la interfaz de línea de comandos (CLI) npm.

- En el sitio web de npm, puede examinar qué paquetes de JavaScript están disponibles en el registro de npm.
- El registro de npm es una gran base de datos de información sobre los paquetes JavaScript disponibles en npm.
- Una vez que haya identificado el paquete que desea, puede usar la npm CLI para instalarlo en su proyecto o globalmente (como otras herramientas de CLI). La CLI de npm es lo que habla con el registro — generalmente solo interactuas con el sitio web o la CLI de npm.

> 💡 Mira la Introducción a npm, “[**Qué es npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Aprende más sobre Git

No tienes que saber Git para completar este tutorial, pero es una herramienda muy util. Si estás interesado en aprender sobre control de versiones, Git y Github, mira el [Git Handbook](https://guides.github.com/introduction/git-handbook/).
