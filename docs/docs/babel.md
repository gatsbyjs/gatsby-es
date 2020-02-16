---
title: Babel
---

Gatsby usa el proyecto fenomenal llamado [Babel](https://babeljs.io/) para tener
compatibilidad y poder escribir JavaScript moderno, sin dejar de soportar navegadores antiguos.

## Como especificar cuales navegadores soportar

Gatsby soporta por defecto las últimas dos versiones de los navegadores principales, 
IE 9+, así como cualquier navegador que aún tenga el 1%+ de la cuota de navegación.

Esto significa que compilamos automáticamente tu Javascript para garantizar que funcione en navegadores antiguos.
También, agregamos automáticamente los polyfills que sean necesarios, no más códigos de envío 
que se rompen misteriosamente en navegadores antiguos!

Si tú solo le apuntas a los navegadores más nuevos. Revisa la página de  
la documentación [Compatibilidad Con Navegadores](/docs/browser-support/) para 
conocer como indicarle a Gatsby qué navegadores soportas y entonces Babel 
comenzará a compilar solo para esos navegadores

## Como usar un archivo .babelrc personalizado

Gatsby viene con una configuración .babelrc por defecto que debería funcionar para la mayoría de los sitios.
Si tú quisieras agregar presets o plugins de Babel personalizados, puedes crear tu propio .babelrc en la raíz 
de tu sitio, importa [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby), 
y agrega los plugins, presets y pass options de Babel a `babel-preset-gatsby`, p. ej. `targets`.

```shell
npm install --save-dev babel-preset-gatsby
```

<!-- prettier-ignore-start -->
```json:title=.babelrc
{
  "plugins": ["@babel/plugin-proposal-optional-chaining"],
  "presets": [
    [
      "babel-preset-gatsby",
      {
        "targets": {
          "browsers": [">0.25%", "no está muerto"]
        }
      }
    ]
  ]
}
```
<!-- prettier-ignore-end -->

Para configuraciones más avanzadas, también puedes copiar los valores predeterminados de [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) y personalizarlos para satisfacer tus necesidades. 
