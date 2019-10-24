---
title: Usando Gitpod, un ambiente de desarrollo Online
---

Esta página resume como usar Gitpod, un ambiente de desarrollo Online gratuito, para contribuir al core de Gatsby y a su ecosistema. Para obtener instrucciones sobre cómo configurar un entorno de desarrollo localmente, visita la página de [configuración local](/contributing/setting-up-your-local-dev-environment/).

## Sobre Gitpod

Gitpod facilita las contribuciones en GitHub, al permitir configuraciones de entornos de desarrollo automatizados. En lugar de escribir mucha documentación de como instalar, configurar y dejar que cada contribuidor pase por esta aventura, la configuración es automática y reproducible.

Además, Gitpod pre-compila cada rama del repositorio, para que no tengas que esperar la instalación, la clonación y la compilación.

## Para empezar

Para iniciar un nuevo entorno de desarrollo, puedes prefijar cualquier URL de GitHub con `gitpod.io/#`.

> Ejemplo: https://gitpod.io/#https://github.com/gatsbyjs/gatsby

El entorno de desarrollo iniciado, se abrirá con un proyecto core de Gatsby listo para usar, así como con un ejemplo integrado (gatsbygram).

Se inician tres terminales en paralelo, ejecutando los siguientes procesos:

- `yarn run watch --scope={gatsby,gatsby-image,gatsby-link}`
  Observa y reconstruye el código core de gatsby en cualquier cambio
- `gatsby-dev`
  Copias sobre los cambios del core al ejemplo
- `gatsby develop`
  Sirve un ejemplo en modo desarrollo

El ejemplo que se está ejecutando se muestra a la derecha en una ventana de vista previa.

## Trabajando en un issue

Para empezar a trabajar en un issue, puedes prefijar la URL del issue con `gitpod.io/#`.

> Ejemplo: https://gitpod.io/#https://github.com/gatsbyjs/gatsby/issues/1199

Esto abrirá un nuevo entorno con una rama local con el nombre del issue.
Ahora puedes codificar, probar, consolidar (commit), mandar (push) y crear un PR desde el espacio de trabajo.

## Revisiones de código

Algunos cambios en el código requieren una revisión más profunda de lo que es posible mostrar en GithHub. Prefijar un PR con `gitpod.io/#` abrirá esa rama en modo de revisión de código.

En este modo, puedes ver la lista de cambios de archivos a la izquierda y puedes navegar a través de ellos. Puedes ejecutar la aplicación y usar las funciones de edición para explorar el código fuente modificado. Además de ver los comentarios existentes o agregar nuevos comentarios en el editor y enviar el resultado de tu revisión.

## Cómo ejecutar otro ejemplo

Si quieres ejecutar otro ejemplo, puedes abrir la terminal o usar una existente y ejecutar los siguientes comandos:

```shell
yarn install
gatsby-dev --set-path-to-repo ../..
gatsby-dev
yarn run dev
```
