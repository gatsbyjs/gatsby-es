---
title: Creación de un Blog de Gatsby con Netlify CMS
---

https://youtu.be/JeTqxCJC56Q

Este tutorial usará [gatsby-personal-starter-blog](http://t.wang.sh/gatsby-personal-starter-blog), un proyecto inicial de Gatsby basado en el oficial [gatsby-starter-blog](/starters/gatsbyjs/gatsby-starter-blog/). Las diferencias son que `gatsby-personal-starter-blog` está configurado para ejecutar el blog en un subdirectorio, `/blog`, y viene preinstalado con [Netlify CMS](https://www.netlifycms.org/) para edición de contenidos. También agrega el resaltado de código de VS Code para bloques de código.

## Prerrequisitos

- Una cuenta de GitHub
- [Gatsby CLI](/docs/gatsby-cli) instalada en tu equipo

## Configuración de un sitio Gatsby administrado por Netlify CMS en 5 pasos:

### Paso 1

Abre tu Terminal y ejecuta el siguiente comando desde la CLI de Gatsby para crear un nuevo sitio de Gatsby usando [gatsby-personal-starter-blog](http://t.wang.sh/gatsby-personal-starter-blog).

```shell
gatsby new [nombre-de-tu-proyecto] https://github.com/thomaswangio/gatsby-personal-starter-blog
```

### Paso 2

Una vez que el sitio de Gatsby haya terminado de instalar todos los paquetes y dependencias, podrás ir al directorio y ejecutar el sitio localmente.

```shell
cd [nombre-de-tu-proyecto]
gatsby develop
```

<<<<<<< HEAD
Ahora puedes ir a [`localhost:8000`](http://localhost:8000) para ver tu nuevo sitio, pero lo que es genial es que Netlify CMS está preinstalado y puedes acceder a él en [`localhost:8000/admin`](http://localhost:8000/admin).
=======
Now you can go to `http://localhost:8000` to see your new site, but what's extra cool is that Netlify CMS is pre-installed and you can access it at `http://localhost:8000/admin`
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Un CMS, o sistema de administración de contenido, es útil porque puedes agregar contenido como publicaciones de blog desde un tablero en tu sitio, en lugar de tener que agregar publicaciones manualmente con Markdown. Sin embargo, es probable que desees poder acceder al CMS desde un sitio web desplegado, no solo localmente. Para eso deberás desplegar en Netlify a través de GitHub, preparar una implementación continua y realizar algunas configuraciones. Repasaremos esto en el [Paso-5](#step-5).

### Paso 3

Abre el proyecto en tu editor de código y luego el archivo `static/admin/config.yml`. Reemplaza `tu-nombre-de-usuario/tu-nombre-de-repositorio` con tu nombre de usuario y de proyecto de GitHub. Este paso es importante para administrar e implementar la interfaz de Netlify CMS.

```diff
backend:
-  name: test-repo

+  name: github
+  repo: tu-nombre-de-usuario/tu-nombre-de-repositorio
```

#### Personalizando tu sitio

Accede a `gatsby-config.js` y edita tu siteMetadata. Añade tu ID de Google Analytics y tu icono/favicon. Prueba los cambios para la compilación implementada saliendo del servidor de desarrollo y ejecutando  `gatsby build && gatsby serve`.

Probablemente también quieras editar el `README.md` y el `package.json`, archivos para incluir tus propios detalles del proyecto.

### Paso 4

<<<<<<< HEAD
Abre [github.com](http://github.com) y crea un nuevo repositorio, con el mismo nombre que tu proyecto. Inserta el código de tu nuevo sitio Gatsby en GitHub usando los siguientes comandos de Terminal:
=======
Open [github.com](https://github.com) and create a new repository, with the same name as your project. Push your new Gatsby site's code to GitHub using the following Terminal commands:
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
git init
git add .
git commit -m "initial commit"
git remote add origin https://github.com/[tu-nombre-de-usuario]/[tu-nombre-de-repositorio].git
git push -u origin master
```

Luego abre [app.netlify.com](http://app.netlify.com) y añade un "Nuevo sitio de Git". Elige tu repositorio recién creado y haz clic en "Desplegar sitio" con la configuración de implementación predeterminada.

> _Nota: si no ves el repositorio correcto en la lista, es posible que debas instalar o volver a configurar la aplicación Netlify en GitHub._

![Tablero de Netlify para Crear un nuevo sitio](netlify-dashboard.png)

### Paso 5

Para asegurarse de que Netlify CMS tenga acceso a tu repositorio de GitHub, debes configurar una aplicación OAuth en GitHub. Las instrucciones para eso están aquí: [Uso de un Proveedor de Autorización con Netlify](https://www.netlify.com/docs/authentication-providers/#using-an-authentication-provider).

Para la "URL de la página de inicio": puedes usar tu subdominio de Netlify, `[nombre-de-tu-sitio].netlify.com`, o puedes usar un dominio personalizado. Para personalizar el subdominio, busca el campo "Editar nombre del sitio" en "Administración del dominio" para tu proyecto en la [App de Netlify](https://app.netlify.com). Para conectar tu sitio de Netlify a tu dominio personalizado, consulta las [Instrucciones para dominios personalizados en Netlify](https://www.netlify.com/docs/custom-domains/).

Una vez que hayas configurado un proveedor de autenticación, podrás usar Netlify CMS en tu sitio implementado para agregar nuevas publicaciones.

![Autorización de Netlify y GitHub](https://cdn.netlify.com/67edd5b656c432888d736cd40125cb61376905bb/c1cba/img/docs/github-oauth-config.png)

Copia las credenciales de tu nueva aplicación listada en [Apps de oAuth en GitHub](https://github.com/settings/developers) e instala un nuevo proveedor de autenticación en Netlify usándolas.

![Configurar el control de acceso](netlify-install-oauth-provider.png)

#### Beneficios de Netlify CMS, GitHub y Netlify Workflow

¡Felicidades! Ahora que Netlify CMS está configurado correctamente para tu proyecto, cada vez que agregues una nueva publicación, el contenido se almacenará en tu repositorio y se versionará en GitHub porque Netlify CMS está basado en Git. Además, gracias a la [Implementación Continua de Netlify](https://www.netlify.com/docs/continuous-deployment/), se implementará una nueva versión cada vez que agregues o edites una publicación.

Puedes obtener más información sobre Netlify CMS y cómo configurarlo de más formas en la [Documentación de Netlify CMS](https://www.netlifycms.org/docs/intro/).
