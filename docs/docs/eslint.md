---
title: Usando ESLint
---

ESLint es una utilidad de linting para JavaScript de código abierto. El linting de código es un tipo de análisis estático que se utiliza con frecuencia para encontrar patrones problemáticos. Hay linters de código para la mayor parte de lenguajes de programación, y los compiladores a veces incorporan linting en el proceso de compilación.

JavaScript, siendo un lenguaje dinámico y de tipado débil, es especialmente propenso a errores por parte de los desarrolladores. Sin el beneficio de un proceso de compilación, JavaScript típicamente se ejecuta para encontrar errores de sintáxis y otros errores. Herramientas de linting como ESLint permiten a los desarrolladores descubrir problemas con su código JavaScript sin ejecutarlo.

## Cómo utilizar ESLint

Gatsby cuenta con una configuración de ESLint incorporada por defecto. Para muchos usuarios, nuestra configuración es lo único que necesitas. Sin embargo, si sabes que te gustaría personalizar tu configuración de ESLint; como por ejemplo, si tu compañía tiene su propia configuración; esto muestra cómo se puede hacer.

We'll replicate (mostly) the [ESLint config Gatsby ships with](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.js) so you can then add additional presets, plugins, and rules.

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
