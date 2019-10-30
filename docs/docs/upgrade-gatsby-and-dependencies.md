---
title: Actualizar para lanzamientos parche o menores
---
Para mantenerte actualizado con los últimos arreglos, parches de seguridad y lanzamientos menores de Gatsby y sus dependencias, debes actualizar constantemente a las últimas versiones de cada paquete.

## Versionado Semántico

Como muchos otros paquetes, Gatsby usa [versionado semántico](https://semver.org/) para etiquetar nuevas versiones e indicar el tipo de cambio que se introduce en cada lanzamiento.

Esta guía busca enseñarte cómo actualizar Gatsby para lanzamientos parche o menores. Para actualizaciones mayores, puedes ir al índice de guías de referencia para [Lanzamientos y  Migraciones](/docs/releases-and-migration/) donde encontrarás la guía correspondiente de actualización.

## ¿Por qué deberías actualizar Gatsby y sus dependencias?

Cada nueva versión de cada paquete viene con mejoras en múltiples áreas como rendimiento, accesibilidad, seguridad, arreglo de bugs y más, de manera que es importante actualizar tanto Gatsby como sus dependencias para obtener las últimas mejoras en cada una de estas áreas.

Actualizar tus dependencias en lanzamientos parche o menores también ayuda a que actualizar a lanzamientos mayores sea más fácil, además de que te ayuda a identificar funcionalidades y APIs que se volverán obsoletas en futuros lanzamientos

## Cómo identificar posibles actualizaciones

Para comenzar, ejecuta el comando `outdated` de npm, para identificar nuevas actualizaciones de tus dependencias.

```shell
npm outdated
```

Este comando imprimirá una tabla indicando qué paquetes tienen nuevas versiones disponibles y cuál es la última versión para cada uno.

```
Package                            Current   Wanted   Latest  Location
gatsby                             2.15.13  2.15.13  2.15.20
```

## Configurar tus dependencias para actualizarse

Dependiendo de si quieres actualizar Gatsby y sus dependencias para actualizaciones parche o menores, necesitas modificar tu `package.json` apropiadamente.

Si solo quieres actualizar para **actualizaciones parche**, puedes agregar una tilde (`~`) antes de cada versión en tu archivo `package.json`

```json:title=package.json
"dependencies"{
  "gatsby": "~2.15.13",
}
```

Agrega un signo de intercalación (`^`) antes de cada versión para ambas **actualizaciones parche y menores**

```json:title=package.json
"dependencies"{
  "gatsby": "^2.15.13",
}
```
Para actualizaciones mayores, usa la guía correspondiente del índice de guías de referencia para [Lanzamientos y Migraciones](/docs/releases-and-migration/)

Si estás actualizando Gatsby, probablemente también necesites  actualizar los plugins que Gatsby mantiene. Puedes identificarlos por su nombre que comienza con `gatsby-`. Recuerda, esto solo aplica para plugins administrados en el repositorio [gatsbyjs/gatsby](https://github.com/gatsbyjs/gatsby); para plugins administrados por la comunidad, verifica si hay una nueva versión a la que puedas actualizar.

## Actualizar todas las dependencias en conjunto

Luego de agregar las anotaciones correspondientes en tu archivo `package.json`, puedes ejecutar el commando `update` de npm.

```shell
npm update
```

Este comando actualizará todos tus paquetes a la última [versión requerida](https://docs.npmjs.com/cli/outdated), ya sea la última actualización parche, menor o mayor, dependiendo de las anotaciones en el `package.json`. 

## Actualizar dependencias individualmente

También puedes actualizar tus dependencias una a la vez con el comando `install` de npm, junto con la versión que quieras instalar o a la que quieras actualizar.

```shell
npm install <paquete>@<version> --save
```

Puedes especificar la versión que quieres instalar o a la que quieres actualizar en cualquiera de los siguientes formatos:

- Una versión específica luego del carácter `@`
- Una versión anotada con `*`,`^`,`~` para indicar que requieres la última actualización mayor, menor o de parche respectivamente.
- Usa una `x` en lugar de un número para indicar que quieres la última actualización mayor (`x`), menor (`<major>.x`) o de parche (`<major>.<minor>.x`). Por ejemplo, para instalar la última actualización parche y especificar una versión mayor y menor, usa el siguiente formato: `npm install package-name@2.1.x --save`

Recuerda que para actualizaciones mayores debes seguir la guía correspondiente del índice de guías de referencia para [Lanzamientos y Migraciones](/docs/releases-and-migration/)

## Actualizaciones interactivas

Puedes seleccionar individualmente qué dependencias quieres actualizar a través del módulo [npm-check](https://www.npmjs.com/package/npm-check). Para hacer esto, inicia instalando el siguiente módulo.

```shell
npm install npm-check --save-dev
```

Posteriormente, agrega el script correspondiente en tu archivo `package.json`.

```json:title=package.json
{
  "scripts": {
    "upgrade-interactive": "npm-check --update"
  }
}
```

Finalmente, ejecuta el comando que agregaste recientemente en los scripts:

```shell
npm run upgrade-interactive
```

## Solución de problemas

Aparte de casos muy específicos como [Gatsby abandonando el soporte para Node 6](/blog/2019-06-18-dropping-support-for-node-6/), actualizar para lanzamientos parche o menores no debería requerir modificaciones a tu código. Se recomienda que corras tu suite de pruebas (en caso de que tengas una), luego de actualizar Gatsby o sus dependencias.

En caso de que te encuentres con conflictos de versiones en tus dependencias, puedes usar el módulo [npm-force-resolutions](https://www.npmjs.com/package/npm-force-resolutions?activeTab=readme)

## Contenido relacionado

Revisa estas guías que cubren actualizaciones mayores de Gatsby:

- [Migrando de v1 a v2](/docs/migrating-from-v1-to-v2/)
- [Migrando de v0 a v1](/docs/migrating-from-v0-to-v1/)
