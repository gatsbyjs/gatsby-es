---
título: Utilización ESLint
---

ESLint es una utilidad de linting JavaScript de código abierto. El linting de código es un tipo de análisis estático que se utiliza con frecuencia para encontrar patrones problemáticos. Hay código linters para la mayor parte de lenguajes de programación, y los compiladores a veces incorporan linting en el proceso de compilación.

JavaScript, siendo un lenguaje dinámico y de tipo suelto, es especialmente propenso a errores de desarrollador. Sin el beneficio de un proceso de compilación, JavaScript el código es típicamente ejecutado a fin de encontrar la sintaxis u otros errores. Herramientas de linting como ESLint permiten a los desarrolladores descubrir problemas con su código JavaScript sin ejecutarlo.

## Cómo utilizar ESLint

Gatsby buques con un built-in [ESLint](https://eslint.org) setup. Para usuarios _most_, nuestra configuración ESLint incorporada es todo lo que necesita. Si sabe sin embargo que le gustaría personalizar su ESLint config e.g. su compañía tiene su propio sistema de ESLint de encargo, esto muestra cómo esto puede ser hecho.

Replicaremos (principalmente) el [ESlint config Gatsby ships with](https://github.com/gatsbyjs/gatsby/blob/master/.eslintrc.json) por lo que puede agregar ajustes preestablecidos adicionales, plugins y reglas.

```shell

# Primero instale las dependencias necesarias de ESLint
npm install --save-dev eslint-config-react-app
```

Ahora que tenemos nuestros paquetes instalados, crear un nuevo archivo en la raíz del sitio denominado `.eslintrc.js` usando el siguiente comando.

```shell
# Crear un archivo de configuración para ESLint
touch .eslintrc.js
```

### Configuración de ESLint

Copie el siguiente fragmento al recién creado `.eslintrc.js` archivo. A continuación, agregue ajustes preestablecidos, plugins y reglas adicionales como desee.

```js:title=.eslintrc.js
module.exports = {
  globals: {
    __PATH_PREFIX__: true,
  },
  extends: `react-app`,
}
```
