---
title: Depuración de problemas de caché
---

Puede haber ciertos escenarios en los que el mecanismo de almacenamiento en caché de Gatsby parece fallar, lo que puede conducir a problemas como:

- Contenido que no aparece cuando debería
- Los cambios en el código fuente del plugin no parecen invocarse adecuadamente

¡y más! Si te has encontrado escribiendo un script como:

```json:title=package.json
{
  "scripts": {
    "clean": "rm -rf .cache"
  }
}
```

considera utilizar el comando `gatsby clean` que puede ayudarte a resolver los problemas de almacenamiento en caché.

Primero asegúrate de que la versión de `gatsby` especificada en tus dependencias` package.json` sea _al menos_ `2.1.1`, y luego realiza el siguiente cambio en` package.json`:

```json:title=package.json
{
  "scripts": {
    "clean": "gatsby clean"
  }
}
```

Ahora, cuando surgen problemas que parecen estar relacionados con el almacenamiento en caché, puedes usar `npm run clean` para borrar el caché y comenzar desde un nuevo estado.

_Nota: Si te encuentras usando este comando regularmente, considera ayudarnos y [responder a nuestros issues de GitHub][github-issue] con pasos claros de reproducción ._

[issue de github]: https://github.com/gatsbyjs/gatsby/issues/11747
