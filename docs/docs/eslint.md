---
title: Usando ESLint
---

ESLint es una utilidad de linting para JavaScript de código abierto. El linting de código es un tipo de análisis estático que se utiliza con frecuencia para encontrar patrones problemáticos. Hay linters de código para la mayor parte de lenguajes de programación, y los compiladores a veces incorporan linting en el proceso de compilación.

JavaScript, siendo un lenguaje dinámico y de tipado débil, es especialmente propenso a errores por parte de los desarrolladores. Sin el beneficio de un proceso de compilación, JavaScript típicamente se ejecuta para encontrar errores de sintáxis y otros errores. Herramientas de linting como ESLint permiten a los desarrolladores descubrir problemas con su código JavaScript sin ejecutarlo.

## Cómo utilizar ESLint

Gatsby cuenta con una configuración de ESLint incorporada por defecto. Para muchos usuarios, nuestra configuración es lo único que necesitas. Sin embargo, si sabes que te gustaría personalizar tu configuración de ESLint; como por ejemplo, si tu compañía tiene su propia configuración; esto muestra cómo se puede hacer.

Replicaremos (mayormente) la [configuración que viene incluida en Gatsby](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js) para permitirte agregar presets adicionales, plugins y reglas.

```shell

# Primero instala las dependencias necesarias de ESLint
npm install --save-dev eslint-config-react-app
```

Ahora que tenemos nuestros paquetes instalados, crea un nuevo archivo en la raíz del sitio llamado `.eslintrc.js` usando el comando a continuación.

```shell
# Crear un archivo de configuración para ESLint
touch .eslintrc.js
```

### Configuración de ESLint

Copia el siguiente fragmento al recién archivo creado `.eslintrc.js`. Ahora puedes agregar ajustes predeterminados, plugins y reglas como quieras.

```js:title=.eslintrc.js
module.exports = {
  globals: {
    __PATH_PREFIX__: true,
  },
  extends: `react-app`,
}
```
<<<<<<< HEAD
=======

Note: When there is no ESLint file Gatsby implicitly adds a barebones ESLint loader. This loader pipes ESLint feedback into the terminal window where you are running or building Gatsby and also to the console in your browser developer tools. This gives you consolidated, immediate feedback on newly-saved files. When you include a custom `.eslintrc` file, Gatsby gives you full control over the ESLint configuration. This means that it will override the built-in `eslint-loader` and you need to enable any and all rules yourself. One way to do this is to use the Community plugin [`gatsby-eslint-plugin`](/packages/gatsby-plugin-eslint/). This also means that the default [ESLint config Gatsby ships with](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js) will be entirely overwritten. If you would still like to take advantage of those rules, you'll need to copy them to your local file.

### Disabling ESLint

Creating an empty `.eslintrc` file at the root of your project will disable ESLint for your site. The empty file will disable the built-in `eslint-loader` because Gatsby assumes once you have an ESLint file you are in charge of linting.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc
