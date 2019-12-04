---
title: Cómo funciona Gatsby con _GitHub Pages_
---

_GitHub Pages_ es un servicio ofrecido por GitHub que permite el alojamiento de sitios web configurados directamente desde el repositorio. Un sitio Gatsby se puede alojar en _GitHub Pages_ mediante unas pocas configuraciones al código base y la configuración del repositorio.

Puedes publicar tu sitio en _GitHub Pages_ de diferentes maneras:

- a una ruta como `username.github.io/reponame/` o `/docs`
- a un subdominio basado en tu nombre de usuario o en el nombre de tu organización: `username.github.io` o `orgname.github.io`
- al subdominio raíz en `username.github.io`, y luego configurado para usar un dominio personalizado

## Configurar la rama fuente de _GitHub Pages_

En la configuración de tu repositorio en GitHub, debes seleccionar la rama que se implementará para que funcione _GitHub Pages_. En GitHub:

1. Navega al repositorio de tu sitio.

2. Debajo del nombre del repositorio, haz clic en Configuración.

3. En la sección _GitHub Pages_, usa el menú desplegable Fuente para seleccionar _master_ (para publicar en el subdominio raíz) o _gh-pages_ (para publicar en una ruta como `/docs`) como tu fuente de publicación de _GitHub Pages_.

4. Haz clic en Guardar.

## Instalación del paquete `gh-pages`

La forma más fácil de enviar una aplicación Gatsby a _GitHub Pages_ es mediante el uso de un paquete llamado [gh-pages](https://github.com/tschaub/gh-pages).

```shell
npm install gh-pages --save-dev
```

## Usando un _script_ de despliegue

Un _script_ personalizado en tu `package.json` hace que sea más fácil construir tu sitio y mover el contenido de los archivos construidos a la rama adecuada para _GitHub Pages_, esto ayuda a automatizar ese proceso.

### Implementar en una ruta en _GitHub Pages_

Para sitios implementados en una ruta como `username.github.io/reponame/`, el _flag_ `--prefix-paths` se usa porque tu sitio web terminará dentro de una carpeta como `username.github.io/reponame/`. Tendrás que agregar tu `/reponame` [path prefix](/docs/path-prefix/) como una opción para `gatsby-config.js`:

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: "/reponame",
}
```

Luego agrega un _script_ `deploy` a `package.json` en el código base de tu repositorio:

```json:title=package.json
{
  "scripts": {
    "deploy": "gatsby build --prefix-paths && gh-pages -d public"
  }
}
```

Cuando ejecutes `npm run deploy`, todo el contenido de la carpeta `public` será movido a la rama `gh-pages` de tu repositorio. Asegúrate de que la configuración de tu repositorio tenga la rama `gh-pages` establecida como la fuente desde la cual se hará el despliegue.

**Nota**: para seleccionar _master_ o _gh-pages_ como tu fuente de publicación, debes tener la rama presente en tu repositorio. Si no tienes una rama _master_ o _gh-pages_, puedes crearlas y luego volver a la configuración de fuente para cambiar tu fuente de publicación.

### Implementar en un subdominio de _GitHub pages_ en github.io

Para un repositorio llamado como `username.github.io`, no necesitas especificar `pathPrefix` y tu sitio web debe ser enviado a la rama `master`.

```json:title=package.json
{
  "scripts": {
    "deploy": "gatsby build && gh-pages -d public -b master"
  }
}
```

Una vez ejecutes `npm run deploy` deberías poder ver tu sitio web en `username.github.io`

### Implementar en el subdominio raíz y usar un dominio personalizado

Si usas un [dominio personalizado](https://help.github.com/articles/using-a-custom-domain-with-github-pages/), no agregues un `pathPrefix` ya que impedirá la navegación en tu sitio. El prefijo de ruta solo es necesario cuando el sitio _no_ está en la raíz del dominio como es el caso de los sitios de repositorio.

**Nota**: No olvides agregar tu archivo [CNAME](https://help.github.com/articles/troubleshooting-custom-domains/#github-repository-setup-errors) al directorio `static`.

### Implementar en _GitHub Pages_ desde un servidor CI

También es posible implementar tu sitio web en `gh-pages` a través de un servidor CI. Este ejemplo usa Travis CI, un servicio de _Integración Continua_ alojado, pero otros sistemas de CI también podrían funcionar.

Puedes usar el módulo de npm [gh-pages](https://www.npmjs.com/package/gh-pages) para desplegar. Pero primero, debes configurarlo con las credenciales adecuadas para que `gh-pages` pueda crear una nueva rama.

#### Obtén un _token_ de GitHub para autenticación con CI

Para enviar cambios desde el sistema CI a GitHub, te tendrás que autenticar. Para ello, se recomienda usar [_tokens_ de desarrollador GitHub](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line).

En GitHub, dirígete a las configuraciones de tu cuenta -> Configuraciones de desarollador -> _Tokens_ personales de acceso, y crea un nuevo _token_ que provea los permisos de acceso `repo`.

En las [configuraciones de Travis para el repositorio](https://docs.travis-ci.com/user/environment-variables/#defining-variables-in-repository-settings), agrega una nueva variable de entorno secreta con nombre `GH_TOKEN` con el valor del _token_ copiado de GitHub. Asegúrate de **NO cambiar la configuración "mostrar en registros de compilación" a _on_** ya que el _token_ debe permanecer secreto. De lo contrario, otras personas podrían acceder a tu repositorio (lo que constituye un gran problema de seguridad).

#### Agregar _script_ para desplegar en _GitHub Pages_ a través de CI

Actualiza el `package.json` del proyecto Gatsby para incluir también un script de ejecución `deploy` que llame `gh-pages` con dos argumentos importantes de la línea de comandos:

1. `-d public` - especifica el directorio en el que existen los archivos creados y se enviará como fuente a _GitHub Pages_
2. `-r URL` - la URL del repositorio de GitHub, incluido el uso del _token_ secreto de GitHub (como una variable de entorno secreta) para poder enviar cambios a la rama `gh-pages`, en forma de `https://$GH_TOKEN@github.com/<github username>/<github repository name>.git`

Aquí hay un ejemplo (asegúrate de actualizar los nombres de usuario y repositorio a los tuyos):

```json
  "scripts": {
    "deploy": "gatsby build --prefix-paths && gh-pages -d public -r https://$GH_TOKEN@github.com/lirantal/dockly.git"
  }
```

#### Actualización de la configuración .travis.yml

La siguiente configuración `.travis.yml` provee una referencia:

```yaml
language: node_js
before_script:
  - npm install -g gatsby-cli
node_js:
  - "10"
deploy:
  provider: script
  # Nota: cambia "docs" al directorio donde reside tu sitio gatsby, si es necesario
  script: cd docs/ && yarn install && yarn run deploy
  skip_cleanup: true
  on:
    branch: master
```

Con el fin de desglosar las partes importantes aquí para implementar el sitio web de Gatsby desde Travis a _GitHub Pages_:

1. `before_script` se usa para instalar la CLI de Gatsby para que se pueda usar en el script de ejecución del proyecto para construir el sitio web de Gatsby
2. `deploy` solo se disparará cuando la compilación se ejecute en la rama _master_, en cuyo caso disparará el script de implementación. En el ejemplo anterior, el sitio de Gatsby se encuentra en un directorio `docs/`. El script cambia a ese directorio, instala todas las dependencias del sitio web y ejecuta el script de implementación como se estableció en el paso anterior.

El paso final del proceso será _commit_ y enviar los archivos `.travis.yml` y `package.json` a tu rama base.
