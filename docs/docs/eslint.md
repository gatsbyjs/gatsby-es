---
title: Usando ESLint
---

ESLint es una utilidad de linting para JavaScript de código abierto. El linting de código es un tipo de análisis estático que se utiliza con frecuencia para encontrar patrones problemáticos. Hay linters de código para la mayor parte de lenguajes de programación, y los compiladores a veces incorporan linting en el proceso de compilación.

JavaScript, siendo un lenguaje dinámico y de tipado débil, es especialmente propenso a errores por parte de los desarrolladores. Sin el beneficio de un proceso de compilación, JavaScript típicamente se ejecuta para encontrar errores de sintaxis y otros errores. Herramientas de linting como ESLint permiten a los desarrolladores descubrir problemas con su código JavaScript sin ejecutarlo.

## Cómo utilizar ESLint

Gatsby cuenta con una configuración de ESLint incorporada por defecto. Para muchos usuarios, nuestra configuración es lo único que necesitas. Sin embargo, si sabes que te gustaría personalizar tu configuración de ESLint; como por ejemplo, si tu compañía tiene su propia configuración; esto muestra cómo se puede hacer.

Replicaremos (mayormente) la [configuración que viene incluida en Gatsby](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.ts) para permitirte agregar presets adicionales, plugins y reglas.

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

Copia el siguiente fragmento al recién creado archivo `.eslintrc.js`. Ahora puedes agregar ajustes predeterminados, plugins y reglas como quieras.

```js:title=.eslintrc.js
module.exports = {
  globals: {
    __PATH_PREFIX__: true,
  },
  extends: `react-app`,
}
```

Nota: Cuando no hay un archivo ESLint, Gatsby agrega implícitamente un _loader_ (cargador) en blanco de ESLint. Este _loader_ encola la retroalimentación de ESLint a una ventana de la terminal donde estás ejecutando o construyendo Gatsby y también a la consola de tu navegador, en las herramientas de desarrollo. Esto te da retroalimentación consolidada e inmediata en archivos nuevos guardados. Cuando incluyes un archivo `.eslintrc` personalizado, Gatsby te da control total sobre la configuración de ESLint. Esto significa que sobreescribirá el `eslint-loader` por defecto y que necesitas habilitar cualquiera de las reglas ti mismo. Una forma de hacer esto es con el plugin de la comunidad [`gatsby-eslint-plugin`](/packages/gatsby-plugin-eslint/). Esto también significa que la [configuración por defecto de ESLint con la que Gatsby es descargado](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby/src/utils/eslint-config.ts) será completamente sobreescrita. Sí aun así te gustaría aprovechar la ventaja de estas reglas, necesitarás hacer una copia de ellas a tu archivo local.

### Desactivando ESLint

Crear un archivo `.eslintrc` vacío en la raíz de tu proyecto deshabilitará ESLint de tu sitio. El archivo vacío desactivará el `eslint-loader` por defecto, ya que Gatsby asume que una vez que tienes un archivo ESLint estás a cargo del _linting_.
