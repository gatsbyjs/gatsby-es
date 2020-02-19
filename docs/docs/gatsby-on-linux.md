---
title: Gatsby en Linux
---

<<<<<<< HEAD
# Linux

> Esto es un TODO. Ayuda a nuestra comunidad a expandirlo.

> Por favor utiliza la [Guía de estilo de Gatsby](/contributing/gatsby-style-guide/) para asegurar que tu pull request sea aceptado.

## Windows Subsystem Linux (WSL)

A partir del 17 de octubre de 2017, Windows 10 viene con distribuciones WSL y Linux disponibles a través de la [Windows Store], hay distribuciones diferentes para usar y se pueden configurar a través de `wslconfig` si tienes más de una distribución instalada.
=======
This guide assumes you already have a native installation of Linux on your machine. The following steps walk through how to install Node.js and associated dependencies.

## Ubuntu, Debian, and other `apt` based distros

Begin by updating and upgrading.

```shell
sudo apt update
sudo apt -y upgrade
```

Install cURL which allows you to transfer data and download additional dependencies.

```shell
sudo apt install curl
```

Once `curl` is installed, you can use it to install `nvm`, which will manage `node` and all its associated versions.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Note that this is the current stable release of nvm. Full installation instructions and troubleshooting can be found at the [nvm GitHub page](https://github.com/nvm-sh/nvm)

When `nvm` is installed, it does not default to a particular `node` version. You'll need to install the version you want and give `nvm` instructions to use it. This example uses the latest release of version `10`, but more recent version numbers can be used instead.

```shell
nvm install 10
nvm use 10
```

To confirm this has worked, use the following command.

```shell
node -v
```

> Note that `npm` comes packaged with `node`

Finally, install `git` which will be necessary for creating your first Gatsby project based on a starter.

```shell
sudo apt install git
```

## Fedora, RedHat, and other `dnf` based distros

These distros come installed with `curl`, so you can use that to download `nvm`.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Note that this is the current stable release of nvm. Full installation instructions and troubleshooting can be found at the [nvm GitHub page](https://github.com/nvm-sh/nvm)

When `nvm` is installed, it does not default to a particular `node` version. You'll need to install the version you want and give `nvm` instructions to use it. This example uses the latest release of version `10`, but more recent version numbers can be used instead.

```shell
nvm install 10
nvm use 10
```

To confirm this has worked, use the following command.

```shell
node -v
```

> Note that `npm` comes packaged with `node`

Finally, install `git` which will be necessary for creating your first Gatsby project based on a starter.

```shell
sudo dnf install git
```

## Archlinux and other `pacman` based distros

Begin by updating.

```shell
sudo pacman -Sy
```

These distros come installed with `curl`, so you can use that to download `nvm`.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

> Note that this is the current stable release of nvm. Full installation instructions and troubleshooting can be found at the [nvm GitHub page](https://github.com/nvm-sh/nvm)

Before using `nvm`, you need to install additional dependencies.

```shell
sudo pacman -S grep awk tar git
```

When `nvm` is installed, it does not default to a particular `node` version. You'll need to install the version you want and give `nvm` instructions to use it. This example uses the latest release of version `10`, but more recent version numbers can be used instead.

```shell
nvm install 10
nvm use 10
```

To confirm this has worked, use the following command.

```shell
node -v
```

> Note that `npm` comes packaged with `node`

## Windows Subsystem Linux (WSL)

This guide assumes that you already have WSL installed with a working Linux distro. If you don't, follow [this guide from Microsoft's site](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to install WSL and a Linux distro of your choice.

As of October 17th 2017, Windows 10 ships with WSL and Linux distributions are available via the Microsoft Store, there are several different distributions to use which can be configured via `wslconfig` if you have more than one distribution installed.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
# establece Ubuntu como la distribución predeterminada
wslconfig /setdefault ubuntu
```

<<<<<<< HEAD
### Utilizando Windows Subsystem Linux: Ubuntu
=======
> Please note that if you have used the [Gatsby on Windows](/docs/gatsby-on-windows/) setup without WSL, then you have to delete any existing `node_modules` folder in your project and re-install the dependencies in your WSL environment.

### Using Windows Subsystem Linux: Ubuntu
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Si tienes una instalación fresca de Ubuntu, actualiza:

```shell
sudo apt update
sudo apt -y upgrade
```

<<<<<<< HEAD
> Utiliza el argumento `-y` si estás de acuerdo en actualizar a las últimas versiones de software.

**Herramientas de compilado**
=======
**Build tools**
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

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

### Additional links and resources

- [Super detailed guide to making VSCode work with ESL from VSCode's docs website](https://code.visualstudio.com/docs/remote/wsl)
- [Microsoft Store page for downloading Ubuntu on Windows](https://www.microsoft.com/en-us/store/p/ubuntu/9nblggh4msv6)
- [n](https://github.com/tj/n)
- [nvm](https://github.com/creationix/nvm)
- [n-install](https://github.com/mklement0/n-install)
- [bash startup](https://github.com/Microsoft/WSL/issues/776#issuecomment-266112578)
