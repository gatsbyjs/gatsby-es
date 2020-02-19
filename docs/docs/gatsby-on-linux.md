---
title: Gatsby en Linux
---

# Linux

> Esto es un TODO. Ayuda a nuestra comunidad a expandirlo.

> Por favor utiliza la [Guía de estilo de Gatsby](/contributing/gatsby-style-guide/) para asegurar que tu pull request sea aceptado.

## Windows Subsystem Linux (WSL)

A partir del 17 de octubre de 2017, Windows 10 viene con distribuciones WSL y Linux disponibles a través de la [Windows Store], hay distribuciones diferentes para usar y se pueden configurar a través de `wslconfig` si tienes más de una distribución instalada.

```shell
# establece Ubuntu como la distribución predeterminada
wslconfig /setdefault ubuntu
```

### Utilizando Windows Subsystem Linux: Ubuntu

Si tienes una instalación fresca de Ubuntu, actualiza:

```shell
sudo apt update
sudo apt -y upgrade
```

> Utiliza el argumento `-y` si estás de acuerdo en actualizar a las últimas versiones de software.

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

### Additional links and resources

- [Super detailed guide to making VSCode work with ESL from VSCode's docs website](https://code.visualstudio.com/docs/remote/wsl)
- [Microsoft Store page for downloading Ubuntu on Windows](https://www.microsoft.com/en-us/store/p/ubuntu/9nblggh4msv6)
- [n](https://github.com/tj/n)
- [nvm](https://github.com/creationix/nvm)
- [n-install](https://github.com/mklement0/n-install)
- [bash startup](https://github.com/Microsoft/WSL/issues/776#issuecomment-266112578)
