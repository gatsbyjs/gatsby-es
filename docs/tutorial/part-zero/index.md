---
title: Configura tu Entorno de Desarrollo
typora-copy-images-to: ./
disableTableOfContents: true
---

Antes de comenzar a crear tu primer sitio Gatsby, debes familiarizarte con algunas tecnologías web básicas y asegurarte de haber instalado todas las herramientas de software necesarias.

## Familiarízate con la línea de comandos

La línea de comandos es una interface de texto para ejecutar comandos en tu ordenador. Muchas veces nos referimos a ella como la terminal. En este tutorial lo llamaremos de ambas formas. Es muy parecido a usar el Finder en Mac o el Explorador en Windows. Finder y Explorer son ejemplos de Interfaz gráfica de usuario (GUI). La línea de comandos es una manera poderosa, basada en texto, para interactuar con tu ordenador.

Toma un momento y abre la interfaz de línea de comandos (CLI) de tu computadora. Dependiendo de que sistema operativo estés utilizando, mira las [**instrucciones para Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instrucciones para Windows**](https://www.lifewire.com/how-to-open-command-prompt-2618089) o las [**instrucciones para Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

<<<<<<< HEAD
_Nota: Sí eres nuevo con la línea de comandos, "ejecutar" un comando, significa "escribir una serie de instrucciones en el símbolo del sistema, y oprimir la tecla Enter". Los comandos serán mostrados en una caja destacada, algo como `node --version`, pero no toda caja destacada es un comando! Sí algo es un comando será mencionado como algo que tienes que correr/ejecutar_
=======
_**Note:** If you’re new to the command line, "running" a command, means "writing a given set of instructions in your command prompt, and hitting the Enter key". Commands will be shown in a highlighted box, something like `node --version`, but not every highlighted box is a command! If something is a command it will be mentioned as something you have to run/execute._
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

## Instala Node.js para tu sistema operativo

Node.js es un ambiente que puede ejecutar código Javascript fuera del navegador web. Gatsby esta construído con Node.js. Para ponerte en marcha con Gatsby, necesitarás tener una versión reciente instalada en tu computadora. npm viene junto a Node.js así que sí no tienes npm, probablemente tampoco tienes Node.js.

### Instrucciones para Mac

Para instalar Gatsby y Node.js en una Mac, es recomendado usar [Homebrew](https://brew.sh/). Un poco de configuración al inicio puede evitarte algunos dolores de cabeza despues!

#### Cómo instalar o verificar que tienes instalado Homebrew en tu computadora:

<<<<<<< HEAD
1. Abre tu Terminal.
2. Comprueba sí Homebrew está instalado ejecutando `brew -v`. Deberías ver "Homebrew" y un número de versión.
3. Sí no, descarga e instala [Homebrew con estas instrucciones](https://docs.brew.sh/Installation).
4. Una vez que ya tienes instalado Homebrew, repite el paso 2 para verificar.
=======
1. Open your Terminal.
2. See if Homebrew is installed. You should see "Homebrew" and a version number.

```shell
brew -v
```

3. If not, download and install [Homebrew with the instructions](https://docs.brew.sh/Installation).
4. Once you've installed Homebrew, repeat step 2 to verify.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### Instala las herramientas de línea de comandos de Xcode:

<<<<<<< HEAD
1. Abre tu Terminal.
2. Instala las herramientas de línea de comandos de Xcode ejecutando `xcode-select --install`.
   - Sí eso falla, decargalas [directamente del sitio de Apple](https://developer.apple.com/download/more/), después de iniciar sesión con una cuenta de desarrollador de Apple
3. Después de empezar la instalación, serás llevado de nuevo a aceptar la licensia de software para las herramientas que vas a descargar.
=======
1. Open your Terminal.
2. Install Xcode Command line tools by running:

```shell
xcode-select --install
```

> 💡 If that fails, download it [directly from Apple's site](https://developer.apple.com/download/more/), after signing-in with an Apple developer account.

3. After being prompted to start the installation, you'll be prompted again to accept a software license for the tools to download.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### Instala Node

<<<<<<< HEAD
1. Abre tu Terminal.
2. Ejecuta `brew install node`
   - Sí no quieres instalarlo mediante Homebrew, descarga la última versión de Node.js desde [el sitio oficial de Node.js](https://nodejs.org/es/), haz doble click en el archivo de descarga y sigue las instrucciones de instalación.
=======
1. Open your Terminal
2. Install node with Homebrew:

```shell
brew install node
```

> 💡 If you don't want to install it through Homebrew, download the latest Node.js version from [the official Node.js website](https://nodejs.org/en/), double click on the downloaded file and go through the installation process.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

### Instrucciones para Windows

- Descarga e instala la última versión de Node.js desde [el sitio oficial de Node.js](https://nodejs.org/es/)

### Instrucciones para Linux

Instala nvm (Gestor de versiones de Node) y las dependencias necesarias. nvm es usado para gestionar Node.js y todas sus versiones asociadas.

<<<<<<< HEAD
_💡 Sí cuando instalas un paquete, te pide confirmación, teclea `y` y presiona enter._
=======
> 💡 When installing a package, if it asks for confirmation, type `y` and press enter.

Select your distro:

- [Ubuntu, Debian, and other apt based distros](#ubuntu-debian-and-other-apt-based-distros)
- [Arch, Manjaro and other pacman based distros](#arch-manjaro-and-other-pacman-based-distros)
- [Fedora, RedHat, and other dnf based distros](#fedora-redhat-and-other-dnf-based-distros)

> 💡 If the Linux distribution you are using is not listed here, please find instructions on the web.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### Ubuntu, Debian, y otras distros basadas en `apt`:

<<<<<<< HEAD
1. Ejecuta `sudo apt update` y después `sudo apt -y upgrade` para asegurar que tu distribución de Linux esta lista para lo siguiente.
2. Ejecuta `sudo apt-get install curl` para instalar `curl` que te permite transferir datos y descargar dependencias adicionales.
3. Despues de que termines de instalar todo, ejecuta `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash` para descargar la ultima versión de nvm.
4. Para confirmar que ha funcionado, utiliza el siguiente comando. `nvm --version`. La salida debería ser el número de versión.
5. [Configura la versión por defecto de Node.js](#set-default-nodejs-version)
=======
1. Make sure your Linux distribution is ready to go run an update and an upgrade:

```shell
sudo apt update
sudo apt -y upgrade
```

2. Install curl which allows you to transfer data and download additional dependencies:

```shell
sudo apt-get install curl
```

3. After it finishes installing, download the latest nvm version:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

4. Confirm this has worked. The output should be a version number.

```shell
nvm --version
```

5. Continue with the section: [Set default Node.js version](#set-default-nodejs-version)
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### Arch, Manjaro y otras distros basadas en `pacman`:

<<<<<<< HEAD
1. Ejecuta `sudo pacman -Sy` para asegurarte de que tu distribución esta lista para lo siguiente.
2. Estas distros vienen instaladas con `curl`, así que puedes utilizarlo para descargar nvm.
   `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
3. Antes de utilizar nvm, necesitas instalar unas dependencias adicionales ejecutando `sudo pacman -S grep awk tar`.
4. Para confirmar que ha funcionado, utiliza el siguiente comando. `nvm --version`. La salida debería ser el número de versión.
5. [Configura la versión por defecto de Node.js](#set-default-nodejs-version)
=======
1. Make sure your distribution is ready to go:

```shell
sudo pacman -Sy
```

2. These distros come installed with curl, so you can use that to download nvm:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

3. Before using nvm, you need to install additional dependencies by running:

```shell
sudo pacman -S grep awk tar
```

4. Confirm this has worked. The output should be a version number.

```shell
nvm --version
```

5. Continue with the section: [Set default Node.js version](#set-default-nodejs-version)
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### Fedora, RedHat, y otras distros basadas en `dnf`:

<<<<<<< HEAD
1. Estas distros vienen instaladas con `curl`, así que puedes utilizarlo para descargar nvm.
   `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
2. Para confirmar que ha funcionado, utiliza el siguiente comando. `nvm --version`. La salida debería ser el número de versión.
3. [Configura la versión por defecto de Node.js](#set-default-nodejs-version)

Sí la distribución de Linux que usas no está listada aquí, por favor busca las instrucciones de instalación en la web.
=======
1. These distros come installed with curl, so you can use that to download nvm:

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

2. Confirm this has worked. The output should be a version number.

```shell
nvm --version
```

3. Continue with the section: [Set default Node.js version](#set-default-nodejs-version)
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

#### Configura la versión por defecto de Node.js

<<<<<<< HEAD
Cuando nvm es instalado, no viene configurado con una versión en particular de Node por defecto. Tendrás que instalar la versión que deseas y configurar nvm para que la use. Este ejemplo usa la última versión lanzada de Node 10, pero números de versiones mas recientes pueden ser usados en su lugar.
=======
When nvm is installed, it does not default to a particular node version. You’ll need to install the version you want and give nvm instructions to use it. This example uses the version 10 release, but more recent version numbers can be used instead.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

```shell
nvm install 10
nvm use 10
```

<<<<<<< HEAD
Para confirmar que funcionó, puedes ejecutar `npm --version` y `node --version`. La salida debería verse similar a la captura de pantalla de abajo, mostrando el número de versión en respuesta a los comandos.
=======
Confirm that this worked:

```shell
npm --version
node --version
```

The output should look similar to the screenshot below, showing version numbers in response to the commands.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

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

<<<<<<< HEAD
Gatsby CLI está disponible via npm y debe ser instalado de manera global en tu sistema con el comando `npm install -g gatsby-cli`.
=======
The Gatsby CLI is available via npm and should be installed globally by running:

```shell
npm install -g gatsby-cli
```
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

Para ver los comandos disponibles, ejecuta `gatsby --help`.

<<<<<<< HEAD
![Echa un vistazo a los comandos disponibles con Gatsby](05-gatsby-help.png)
=======
See the available commands:

```shell
gatsby --help
```
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

> 💡 Si no puedes ejecutar la Gatsby CLI por un problema de permisos, quizás te interese mirar [la documentación de npm para solucionar el problema de los permisos (inglés)](https://docs.npmjs.com/getting-started/fixing-npm-permissions), o [ésta guía (inglés)](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Crea un sitio web con Gatsby

Ahora ya estás listo para usar la línea de comandos de Gatsby (Gatsby CLI) para crear tu primer sitio web con Gatsby. Usándola, puedes descargar "plantillas" ("starters") (sitios parcialmente construidos con alguna configuración predeterminada) que te ayudarán a ir más rápido creando cierto tipo de sitios. La plantilla "Hello World" que usarás contiene los elementos básicos necesarios para un sitio web Gatsby.

<<<<<<< HEAD
1. Abre la terminal.
2. Ejecuta `gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world`. (_Nota: Dependiendo de tu velocidad de descarga, el tiempo que ésto tome puede variar. Por razones de brevedad, el siguiente gif se detuvo durante parte de la instalación_)
3.  Ejecuta `cd hello-world`.
4.  Ejecuta `gatsby develop`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

¿Qué ha pasado?
=======
Now you are ready to use the Gatsby CLI tool to create your first Gatsby site. Using the tool, you can download “starters” (partially built sites with some default configuration) to help you get moving faster on creating a certain type of site. The “Hello World” starter you’ll be using here is a starter with the bare essentials needed for a Gatsby site.

1.  Open up your terminal.
2.  Create a new site from a starter:
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

<<<<<<< HEAD
- `new` es un comando de Gatsby para crear un nuevo proyecto Gatsby.
- `hello-world` es un titulo arbitrario — puede ser cualquier cosa. La CLI pondrá el código de tu nuevo sitio web en una nueva carpeta con el nombre "hello-world".
- Por último, la URL de Github especificada apunta a un repositorio de código que almacena la plantilla (starter) que quieres utilizar.
=======
> 💡 What just happened?
>
> - `new` is a gatsby command to create a new Gatsby project.
> - Here, `hello-world` is an arbitrary title — you could pick anything. The CLI tool will place the code for your new site in a new folder called “hello-world”.
> - Lastly, the GitHub URL specified points to a code repository that holds the starter code you want to use.

> 💡 Depending on your download speed, the amount of time this takes will vary. For brevity's sake, the gif below was paused during part of the install

3.  Change into the working directory:
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

```shell
cd hello-world
```

<<<<<<< HEAD
- Esto quiere decir 'Quiero cambiar de directorios (`cd`) al subdirectorio “hello-world”'. Cada vez que quieras ejecutar comandos en tu sitio web, necesitas estar en el contexto del sitio (en otras palabras, la terminal tiene que estar apuntando al directorio donde está el código).
=======
> 💡 This says _'I want to change directories (`cd`) to the “hello-world” subfolder'_. Whenever you want to run any commands for your site, you need to be in the context for that site (aka, your terminal needs to be pointed at the directory where your site code lives).

4.  Start the development mode:
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

```shell
gatsby develop
```

<<<<<<< HEAD
- Éste comando inicia un servidor de desarrollo. Serás capaz de ver e interactuar con tu nuevo sitio web en un entorno de desarrollo — local (en tu ordenador, no publicado a internet).
=======
> 💡 This command starts a development server. You will be able to see and interact with your new site in a development environment — local (on your computer, not published to the internet).

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
  <p>Sorry! Your browser doesn't support this video.</p>
</video>
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

### Mira tu sitio web en local

Abre una nueva pestaña en tu navegador y ve a `http://localhost:8000/`

![Página principal](04-home-page.png)

¡Felicidades! ¡Esto es el inicio de tu primer sitio hecho con Gatsby! 🎉

Puedes ver tu sitio web en local en `http://localhost:8000/` mientras tu servidor de desarrollo esté activo. Este es el proceso que has iniciado cuando ejecutaste el comando `gatsby develop`. Para detener el proceso (o cerrar el servidor de desarrollo), vuelve a la terminal, mantén presionada la tecla "control" y presiona la tecla "c" (ctrl-c). ¡Para iniciarlo nuevamente, ejecuta `gatsby develop` otra vez!

<<<<<<< HEAD
**Nota:** Si estás en un entorno virtual (VM) como `vagrant` y/o te gustaría ejecutara el entorno de desarrollo desde tu dirección IP local, ejecuta `gatsby develop -- --host=0.0.0.0`. Ahora, el servidor de desarrollo escuchará tanto en `http://localhost` como tu dirección IP local.
=======
_**Note:** If you are using VM setup like `vagrant` and/or would like to listen on your local IP address, run `gatsby develop --host=0.0.0.0`. Now, the development server listens on both `http://localhost` and your local IP._
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

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

<<<<<<< HEAD
Para una introducción completa de lo que es un sitio web, --incluida una introducción a HTML y CSS--, mira "[**Building your first web page**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)". Es un gran sitio para comenzar a aprender sobre la web. Para una introducción más práctica a [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css) y [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), consulta los tutoriales de Codecademy. [**React**](https://es.reactjs.org/tutorial/tutorial.html) y [**GraphQL**](http://graphql.org/graphql-js/) también tienen sus propios tutoriales introductorios.
=======
For a comprehensive introduction to what a website is -- including an intro to HTML and CSS -- check out “[**Building your first web page**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. It’s a great place to start learning about the web. For a more hands-on introduction to [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css), and [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), check out the tutorials from Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) and [**GraphQL**](https://graphql.org/graphql-js/) also have their own introductory tutorials.
>>>>>>> 8ff6bb09c23261662f47e79a041a92855d517097

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
