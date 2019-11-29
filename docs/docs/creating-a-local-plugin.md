---
title: Creación de un plugin local
---

Si un plugin es únicamente aplicable a tu caso de uso específico, o si estás desarrollando un plugin y requieres de un flujo de trabajo más sencillo, un plugin definido localmente es la manera más apropiada de crear y gestionar el código de tu plugin.

Coloca el código en la carpeta `plugins` en la carpeta raíz de tu proyecto de esta manera:

```
plugins
└── my-own-plugin
    └── package.json
```

**NOTA:** Aún así necesitas añadir el plugin a tu `gatsby-config.js`. No se detectan automáticamente los plugins locales.

**NOTA:** Para que el plugin sea detectado, el valor del nombre de la carpeta raíz del plugin es el que necesita ser referenciado para poder ser cargado (_no_ el _nombre_ en tu archivo package.json). Para la estructura anterior, por ejemplo, la forma correcta de cargar el plugin es:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: ["my-own-plugin"],
}
```

Como en todos los archivos `gatsby-*`, el código no se procesará por Babel. Si
deseas utilizar sintaxis JavaScript que no es soportada por tu versión de Node.js,
podrás colocar los archivos en un subdirectorio `src` y generarlos en la raíz de
la carpeta del plugin.
