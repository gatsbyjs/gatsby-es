---
title: Gatsby en Linux
---

Esta guía asume que ya tienes una instalación nativa de Linux en tu maquina. Los siguientes pasos te guiarán en cómo instalar Node.js y sus dependencias asociadas.

## Ubuntu, Debian, y otras distros basadas en `apt`

Empieza por actualizar y reemplazar.

```shell
sudo apt update
sudo apt -y upgrade
```

Instala cURL que te permite transferir datos y descargar dependencias adicionales.

```shell
sudo apt install curl
```

Una vez que `curl` está instalado, puedes usarlo para instalar `nvm`, que gestionará `node` y todas sus versiones asociadas.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Ten en cuenta que esta es la versión mas reciente estable de nvm. Las instrucciones de instalación y depuración pueden ser encontradas en la [página de nvm en Github](https://github.com/nvm-sh/nvm)

Cuando `nvm` es instalado, no esta por defecto configurado a una versión en particular de `node`. Necesitarás instalar la versión que quieres y darle instrucciones a `nvm` para usarla. Este ejemplo usa la última versión `10`, pero versiones mas recientes pueden ser usadas en su lugar.

```shell
nvm install 10
nvm use 10
```

Para confirmar que ha funcionado, usa el siguiente comando.

```shell
node -v
```

> Ten en cuenta que `npm` viene empaquetado con `node`

Finalmente, instala `git` que será necesario para crear tu primer proyecto de Gatsby basado en un _starter_.

```shell
sudo apt install git
```

## Fedora, RedHat, y otras distros basadas en `dnf`

Estas distros vienen instaladas con `curl`, así que puedes usarlo para descargar `nvm`.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Ten en cuenta que esta es la versión mas reciente estable de nvm. Las instrucciones de instalación y depuración pueden ser encontradas en la [página de nvm en Github](https://github.com/nvm-sh/nvm)

Cuando `nvm` es instalado, no esta por defecto configurado a una versión en particular de `node`. Necesitarás instalar la versión que quieres y darle instrucciones a `nvm` para usarla. Este ejemplo usa la última versión `10`, pero versiones mas recientes pueden ser usadas en su lugar.

```shell
nvm install 10
nvm use 10
```

Para confirmar que ha funcionado, usa el siguiente comando.

```shell
node -v
```

> Ten en cuenta que `npm` viene empaquetado con `node`

Finalmente, instala `git` que será necesario para crear tu primer proyecto de Gatsby basado en un _starter_.

```shell
sudo dnf install git
```

## Archlinux y otras distros basadas en `pacman`

Empieza por actualizar.

```shell
sudo pacman -Sy
```

Estas distros vienen instaladas con `curl`, así que puedes usarlo para descargar `nvm`.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Ten en cuenta que esta es la versión mas reciente estable de nvm. Las instrucciones de instalación y depuración pueden ser encontradas en la [página de nvm en Github](https://github.com/nvm-sh/nvm)

Antes de usat `nvm`, necesitas instalar unas dependencias adicionales.

```shell
sudo pacman -S grep awk tar git
```

Cuando `nvm` es instalado, no esta por defecto configurado a una versión en particular de `node`. Necesitarás instalar la versión que quieres y darle instrucciones a `nvm` para usarla. Este ejemplo usa la última versión `10`, pero versiones mas recientes pueden ser usadas en su lugar.

```shell
nvm install 10
nvm use 10
```

Para confirmar que ha funcionado, usa el siguiente comando.

```shell
node -v
```

> Ten en cuenta que `npm` viene empaquetado con `node`

## Subsistema Linux de Windows (WSL)

Esta guía asume que ya tienes WSL instalado con una distro Linux funcionando. Sí no, sigue la [guía del sitio de Microsoft](https://docs.microsoft.com/en-us/windows/wsl/install-win10) para instalar WSL y una distro de Linux de tu preferencia.

A partir del 17 de octubre de 2017, Windows 10 viene con distribuciones WSL y Linux disponibles a través de la [Windows Store], hay distribuciones diferentes para usar y se pueden configurar a través de `wslconfig` si tienes más de una distribución instalada.

```shell
# establece Ubuntu como la distribución predeterminada
wslconfig /setdefault ubuntu
```

> Por favor ten en cuenta que sí has usado la instalación de [Gatsby en Windows](/docs/gatsby-on-windows/) sin WSL, entonces tienes que eliminar cualquier carpeta de `node_modules` existente en tu proyecto y re-instalar las dependencias en tu ambiente WSL.
> 
### Utilizando el Subsistema Linux de Windows: Ubuntu

Si tienes una instalación fresca de Ubuntu, actualiza:

```shell
sudo apt update
sudo apt -y upgrade
```

**Herramientas de compilado**

Para compilar e instalar addons nativos desde npm necesitarás instalar herramientas de compilado para `node-gyp`:

```shell
sudo apt install -y build-essential
```

**Instalar node**

Seguir las instrucciones de instalación de nodejs.org acaba con una instalación ligeramente defectuosa (p.e. errores de permisos al intentar ejecutar `npm install`). En su lugar, intenta instalar versiones de node utilizando [n] a través del comando [n-install]:

```shell
curl -L https://git.io/n-install | bash
```

Hay otras alternativas para el manejo de versiones de node, tales como [nvm] pero es sabido que puede afectar la velocidad de [bash startup] en WSL.

### Utilizando Windows Subsystem Linux: Debian

La instalación de Debian es casi indéntica a la de Ubuntu, con la excepción de tener que instalar `git` y `libpng-dev`.

Begin by updating and upgrading.

```shell
sudo apt update
sudo apt -y upgrade
```

Additional dependencies need to be installed as well. `build-essential` is a package that allows other packages to compile to a Debian package. `git` installs a package to work with version control. `linbpng-dev` installs a package that allows the project to manipulate images.

```shell
sudo apt install build-essential
sudo apt install git
sudo apt install libpng-dev
```

O para instalar y aprobar todo al mismo tiempo `(y)`:

```shell
sudo apt update && sudo apt -y upgrade && sudo apt install build-essential && sudo apt install git && sudo apt install libpng-dev
```

### Enlaces adicionales y más recursos

- [Guía super detallada para hacer que VSCode trabaje con ESL de la documentación del sitio web de VSCode](https://code.visualstudio.com/docs/remote/wsl)
- [Página de la tienda de Microsoft para descargar Ubuntu en Windows](https://www.microsoft.com/en-us/store/p/ubuntu/9nblggh4msv6)
- [n](https://github.com/tj/n)
- [nvm](https://github.com/creationix/nvm)
- [n-install](https://github.com/mklement0/n-install)
- [Inicio de bash](https://github.com/Microsoft/WSL/issues/776#issuecomment-266112578)
