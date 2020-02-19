---
title: Babel
---

<<<<<<< HEAD
Gatsby usa el fenomenal proyecto llamado [Babel](https://babeljs.io/) para tener
compatibilidad y poder escribir JavaScript moderno, sin dejar de dar compatibilidad a navegadores antiguos.
=======
Gatsby uses the phenomenal project [Babel](https://babeljs.io/) to enable support for writing modern JavaScript — while still supporting older browsers.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Cómo especificar a cuales navegadores dar compatibilidad

<<<<<<< HEAD
Gatsby es compatible por defecto con las últimas dos versiones de los navegadores principales, 
IE 9+, así como cualquier navegador que aún tenga el 1%+ de la cuota de navegación.

Esto significa que compilamos automáticamente tu Javascript para garantizar que funcione en navegadores antiguos.
También, agregamos automáticamente los `polyfills` que sean necesarios, ¡no más envío de código 
que se rompe misteriosamente en navegadores antiguos!

Si solo le apuntas a los navegadores más nuevos. Revisa la página de  
la documentación [Compatibilidad Con Navegadores](/docs/browser-support/) para 
conocer cómo indicarle a Gatsby con qué navegadores eres compatible y entonces Babel 
comenzará a compilar solo para esos navegadores.
=======
Gatsby supports by default the last two versions of major browsers, IE 9+, as well as any browser that still has 1%+ browser share.

This means that your JavaScript is automatically compiled to ensure it works on older browsers. Polyfills are also automatically added — no more shipping code which mysteriously breaks on older browsers!

If you only target newer browsers, see the [Browser Support](/docs/browser-support/) docs page for how to instruct Gatsby on which browsers you support and then Babel will start compiling for only these browsers.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Cómo usar un archivo .babelrc personalizado

<<<<<<< HEAD
Gatsby viene con una configuración .babelrc por defecto que debería funcionar para la mayoría de los sitios.
Si quisieras agregar presets o plugins de Babel personalizados, puedes crear tu propio `.babelrc` en la raíz 
de tu sitio, importa [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby), 
agrega los plugins y presets adicionales, y pasa las opciones a `babel-preset-gatsby`, p. ej. `targets`.
=======
Gatsby ships with a default .babelrc setup that should work for most sites. If you'd like to add custom Babel presets or plugins, you can create your own `.babelrc` at the root of your site, import [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby), and add additional plugins, presets, and pass options to `babel-preset-gatsby`, e.g. `targets`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

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
          "browsers": [">0.25%", "not dead"]
        }
      }
    ]
  ]
}
```
<!-- prettier-ignore-end -->

Para configuraciones más avanzadas, también puedes copiar los valores predeterminados de [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) y personalizarlos para satisfacer tus necesidades. 
