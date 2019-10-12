---
title: Babel
---

Gatsby usa el fenomenal proyecto [Babel](https://babeljs.io/) para hacer uso de JavaScript moderno
-- mientras seguimos soportando navegadores más viejos.

## ¿Como especificar cual navegador soportar?

Por defecto, Gatsby soporta las últimas dos versiones de los navegadores mayores, IE 9+, así como
cualquier otro navegador que siga teniendo el 1%+ de la cuota de navegadores.

Esto significa que automáticamente compila nuestro JavaScript, para asegurar que funciona con
navegadores más viejos.
También, automáticamente, agregamos polyfills según sea necesario -- evitándonos de crear código que,
misteriosamente, no funciona en navegadores más viejos.

Si lo que buscas es solo soportar los navegadores más nuevos, puedes ir a la documentación de
[Soporte de navegadores](/docs/browser-support/) para ver como indicarle a Gatsby que navegadores
vas a soportar, y Babel comenzará a compilar solo para esos navegadores.

## ¿Como usar un .babelrc personalizado?

Gatsby provee una configuración de .babelrc por defecto, que debería funcionar para la mayoría de
los sitios. Si lo que quieres es agregar presets o plugins de Babel, puedes crear tu
propio `.babelrc` en la raíz de tu proyecto, importar [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby),
y agregar los plugins adicionales, presets y pasar las opciones a `babel-presets-gatsby`, e.g.
`targets`

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

Para configuraciones más avanzadas, puedes copiar los valores por defecto de [`babel-preset-gatsby`](https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby) y personalizarlos para satisfacer tus necesidades.
