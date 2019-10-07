---
título: Usando ESLint
---

ESLint es una utilidad de linting JavaScript de código abierto. El linting de código es un tipo de análisis estático que se utiliza con frecuencia para encontrar patrones problemáticos. Hay linters de código para la mayor parte de lenguajes de programación, y los compiladores a veces incorporan linting en el proceso de compilación.

JavaScript, siendo un lenguaje dinámico y de tipado débil, es especialmente propenso a errores por parte de los desarrolladores. Sin el beneficio de un proceso de compilación, JavaScript típicamente se ejecuta para encontrar errores de sintáxis y otros errores. Herramientas de linting como ESLint permiten a los desarrolladores descubrir problemas con su código JavaScript sin ejecutarlo.

## Cómo utilizar ESLint

Gatsby cuenta con una configuración de ESLint incorporada por defecto. Para muchos usuarios, nuestra configuración es lo único que necesitas. Sin embargo, si sabe que le gustaría personalizar su configuración de ESLint; como por ejemplo, tu compañía tiene su propia configuración ESLint; esto muestra como se puede hacer.

Replicaremos (principalmente) la [configuración que viene incluida en Gatsby] para permitirte agregar presets adicionales, plugins y reglas.

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
