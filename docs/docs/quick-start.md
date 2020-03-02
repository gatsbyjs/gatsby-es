---
title: "Inicio Rápido"
---

Este inicio rápido está destinado a desarrolladores intermedios y avanzados. Para una introducción más suave a Gatsby, [dirígete a nuestro tutorial](/tutorial/)!

## Usa el CLI de Gatsby

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-quick-start-with-gatsby-create-develop-and-build-gatsby-sites-from-the-command-line"
  lessonTitle="Inicio Rápido con Gatsby: Crea, Desarrolla y Construye Sitios Gatsby desde la Línea de Comandos"
/>

**Nota**: este video usa `npx`, la cuál es una herramienta que ejecuta un paquete npm sin instalarlo primero. Ejecutando el comando `npx gatsby new` es lo mismo que ejecutar `gatsby new` después de instalar el gatsby-cli en tu computadora.

### Instalar el CLI de Gatsby.

```shell
npm install -g gatsby-cli
```

> El comando de arriba instala el CLI de Gatsby en tu maquina.

### Crear un nuevo sitio.

```shell
gatsby new gatsby-site
```

### Cambiar el directorio a la carpeta del sitio.

```shell
cd gatsby-site
```

### Iniciar el servidor de desarrollo.

```shell
gatsby develop
```

Gatsby iniciará un entorno de desarrollo con _hot-reloading_ accesible por defecto en `http://localhost:8000`.

Intenta editar las páginas JavaScript en `src/pages`. Los cambios guardados se recargarán en vivo en el navegador.

### Crear una compilación de producción.

```shell
gatsby build
```

Gatsby realizará una compilación de producción para tu sitio, generando HTML estático y paquetes de código JavaScript por ruta.

### Servir la compilación de producción localmente.

```shell
gatsby serve
```

Gatsby inicia un servidor HTML local para probar tu sitio compilado. Recuerda compilar tu sitio usando `gatsby build` antes de usar este comando.

### Accede a la documentación sobre los comandos del CLI

Para ver la documentación detallada sobre los comandos del CLI, ejecuta `gatsby --help` en la terminal.

Para comandos específicos, ejecuta `gatsby COMMAND_NAME --help` p. ej. `gatsby new --help`.

Para más información sobre la CLI de Gatsby, visita la sección [referencia CLI](/docs/gatsby-cli/) de la documentación.
