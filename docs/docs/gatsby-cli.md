---
title: Comandos (Gatsby CLI)
tableOfContentsDepth: 2
---

La interfaz de línea de comandos de Gatsby (CLI) es la manera más fácil de conseguir levantar y hacer funcionar una aplicación de Gatsby y de usar funcionalidades como lanzar un servidor de desarrollo o desplegar tu aplicación de Gatsby.

_Puedes encontrar disponible documentación similar en el [README](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli/README.md) de gatsby-cli, y nuestra [hoja de trucos](/docs/cheat-sheet/) tiene todos los comandos principales de la CLI para que los consultes rápidamente._

## Cómo utilizar gatsby-cli

La CLI de Gatsby (`gatsby-cli`) está empaquetada como un ejecutable que puede usarse globalmente. La CLI de Gatsby está disponible a través de [npm](https://www.npmjs.com/) y debe instalarse globalmente con el comando `npm install -g gatsby-cli` para poder usarla en local.

Introduce `gatsby --help` para ver toda la ayuda.

También puedes usar la variante en script de estos comandos en el `package.json`, normalmente ya expuestos en la mayoría de [_starters_](/docs/starters/). Por ejemplo, si quisiesemos hacer que el comando [`gatsby develop`](#develop) esté disponible en nuestra aplicación, deberíamos abrir el `package.json` y añadir un script como el siguiente:

```json:title=package.json
{
  "scripts": {
    "develop": "gatsby develop"
  }
}
```

## Comandos de la API

### `new`

```shell
gatsby new [<site-name> [<starter-url>]]
```

#### Argumentos

| Argumentos  | Descripción                                                                                                                                                                                                                                                  |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| site-name   | El nombre de tu sitio Gatsby, el cual también se usa para crear el directorio del proyecto.                                                                                                                                                                  |
| starter-url | La URL de un starter de Gatsby o una ruta de archivo local. Por defecto se usa [gatsby-starter-default](https://github.com/gatsbyjs/gatsby-starter-default); Para más información, mira los documentos sobre [_starters_ de Gatsby](/docs/starters/). |

> Nota: El `site-name` solo puede contener letras y números. Si introduces  `.`, `./` o `<espacio>` en el nombre, `gatsby new` lanzará un error.

#### Ejemplos

- Crea un sitio Gatsby con el nombre `my-awesome-site` usando el starter por defecto:

```shell
gatsby new my-awesome-site
```

- Crea un sitio Gatsby con el nombre `my-awesome-blog-site`, usando [gatsby-starter-blog](https://www.gatsbyjs.org/starters/gatsbyjs/gatsby-starter-blog/):

```shell
gatsby new my-awesome-blog-site https://github.com/gatsbyjs/gatsby-starter-blog
```

- Si no introduces ninguno de los argumentos, la CLI te mostrará una _shell_ interactiva para que lo hagas:

```shell
gatsby new
? What is your project called? › my-gatsby-project
? What starter would you like to use? › - Use arrow-keys. Return to submit.
❯  gatsby-starter-default
   gatsby-starter-hello-world
   gatsby-starter-blog
   (Use a different starter)
```

Puedes mirar los [documentos para _starters_ de Gatsby](https://www.gatsbyjs.org/docs/gatsby-starters/) para más detalles.

### `develop`

Una vez ya hayas instalado un sitio de Gatsby, ve al directorio raíz de tu proyecto y lanza el servidor para desarrollo:

`gatsby develop`

#### Opciones

|     Opción      | Descripción                                      |
| :-------------: | ------------------------------------------------ |
| `-H`, `--host`  | Establece el _host_. Por defecto _localhost_     |
| `-p`, `--port`  | Establece el puerto. Por defecto `env.PORT` u 8000            |
| `-o`, `--open`  | Abre por ti el sitio en tu navegador por defecto.|
| `-S`, `--https` | Usa HTTPS                                        |

Sigue la [guía para HTTPS en local](/docs/local-https/)
para averiguar cómo levantar un servidor de desarrollo HTTPS usando Gatsby.

#### Visualiza los cambios en otros dispositivos

Puedes usar el comando _develop_ de Gatsby con la opción de _host_ para acceder a tu entorno de desarrollo desde otros dispositivos conectados a la misma red, ejecuta:

```shell
gatsby develop -H 0.0.0.0
```

El terminal the mostrará la información como normalmente, pero además va a incluir una URL que podrás usar para navegar desde un cliente de la misma red para ver cómo se renderiza.

```shell
You can now view gatsbyjs.org in the browser.
⠀
  Local:            http://0.0.0.0:8000/
  On Your Network:  http://192.168.0.212:8000/ // highlight-line
```

**Nota**: Para acceder a Gatsby en tu maquina local, utiliza `http://localhost:8000` o la URL "En tu red".

### `build`

En el directorio raíz de un sitio de Gatsby, compila tu aplicación y déjala lista para desplegar:

`gatsby build`

#### Opciones

|            Opción            | Descripción                                                                                                                                       |
| :--------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------- |
|       `--prefix-paths`       | Compila tu sitio con una ruta prefijada en los enlaces (establece el _pathPrefix_ en tu configuración)                                            |
|        `--no-uglify`         | Compila tu sitio sin afear los paquetes JS (para propósitos de _debugging_)                                                                       |
|         `--profile`          | Compila tu sitio con `react profiling`. Mira [Midiendo el rendimiento de un sitio con React Profiler](/docs/profiling-site-performance-with-react-profiler/) |
| `--open-tracing-config-file` | Fichero de configuración del _tracer_ (compatible con OpenTracing). Mira la sección sobre [_Tracing_ del Rendimiento](/docs/performance-tracing/) |
| `--no-color`, `--no-colors`  | Deshabilita la interfaz en color                                                                                                                  |

Además de estas opciones, también se pueden establecer [variables de entorno para la compilación](/docs/environment-variables/#build-variables) para una configuración más avanzada que se ajuste mejor a la ejecución de la compilación. Por ejemplo, si establecemos `CI=true` como una variable de entorno conseguiremos una salida a medida para [terminales _dumb_](https://en.wikipedia.org/wiki/Computer_terminal#Dumb_terminals).

### `serve`

En el directorio raíz de un sitio Gatsby, sirve tu proyecto en producción para poder probarlo:

`gatsby serve`

#### Opciones

|      Opción      | Descripción                                                                                                        |
| :--------------: | ------------------------------------------------------------------------------------------------------------------ |
|  `-H`, `--host`  | Establece el _host_. Por defecto _localhost_                                                                       |
|  `-p`, `--port`  | Establece el puerto. Por defecto 9000                                                                              |
|  `-o`, `--open`  | Abre por ti el sitio en tu navegador por defecto                                                                   |
| `--prefix-paths` | Sirve el sitio con rutas prefijadas en los enlaces (si has compilado usando _pathPrefix_ en tu gastsby-config.js). |

### `info`

En el directorio raíz de un sitio Gatsby, recopila información útil que te será requerida cuando reportes un bug:

`gatsby info`

#### Opciones

|       Opción        | Descripción                                                      |
| :-----------------: | ---------------------------------------------------------------- |
| `-C`, `--clipboard` | Copia automagicamente la información del entorno al portapapeles |

### `clean`

En el directorio raiz de un sitio Gatsby, elimina el cache (carpeta `.cache`) y los directorios públicos:

`gatsby clean`

Es muy útil como último recurso cuando tu proyecto local tiene problemas o si el contenido no se refresca. Algunos problemas comunes que puede resolver son:

- Información obsoleta, p. ej. este archivo/recurso/etc. no está disponible
- Error de GraphQL, p. ej. el recurso de GraphQL debería estar presente pero no lo está
- Problemas de dependencias, p. ej. versión invalida, errores crípticos en la consola, etc.
- Problemas de _plugins_, p. ej. desarrollar un _plugin_ local y no ver ningún cambio aplicado

### `plugin`

Ejecuta comandos relacionados con los _plugins_ de gatsby.

#### `docs`

`gatsby plugin docs`

Te dirige a la documentación sobre cómo usar y crear _plugins_.

### Repl

Usa una REPL de Node.js (una _shell_ interactiva) con contexto de tu entorno Gatsby:

`gatsby repl`

Gatsby te permitirá introducir comandos y explorar. Cuando muestre esto: `gatsby >`

Puedes introducir un comando, como alguno de los siguientes:

`babelrc`

`components`

`dataPaths`

`getNodes()`

`nodes`

`pages`

`schema`

`siteConfig`

`staticQueries`

Si se combinan con el [explorador de GraphQL](/docs/introducing-graphiql/), estos comandos REPL pueden ser muy útiles para ayudarte a entender la información de tu sitio Gatsby.

Para más información, echa un vistazo a la [Documentación de Gatsby REPL](/docs/gatsby-repl/).

### Deshabilitar la interfaz en color

Además de la opción explícita `--no-color`, la CLI respeta la presencia de la variable de entorno `NO_COLOR` (mira [no-color.org](https://no-color.org/)).
