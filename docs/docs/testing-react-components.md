---
title: "Testeando componentes React"
---

_El framework de testeo recomendado es [Jest](https://jestjs.io/). Esta guía asume que seguiste la guía de [testeo unitario](/docs/unit-testing) para configurar Jest._

El [@testing-library/react](https://github.com/testing-library/react-testing-library) de Kent C. Dodds ha aumentado en popularidad desde que fue lanzado y es un gran reemplazo para [enzyme](https://github.com/airbnb/enzyme). Puedes escribir tests unitarios y de integración y te incita a consultar el DOM de la misma forma que haría el usuario. De ahí el principio rector:

> _The more your tests resemble the way your software is used, the more confidence they can give you._ (Cuanto más se parezcan sus pruebas a la forma en que se utiliza su software, más confianza le pueden brindar.)

Proporciona funciones ligeras de utilidad además de `react-dom` y `react-dom/test-utils` y te dá la confianza de que no rompe tus test al refactorizar el componente en la implementación (pero no en la funcinalidad).  

## Instalación

Instala la librería como uno de tus proyectos `devDependencies`. Opcionalmente puedes instalar `jest-dom` para usar sus [custom jest matchers](https://github.com/testing-library/jest-dom#custom-matchers).

```shell
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

Crea el archivo `setup-test-env.js` en la raíz de tu proyecto. Introduce este codigo en el:

```js:title=setup-test-env.js
import "@testing-library/jest-dom/extend-expect"
```

Este archivo es automáticamente ejecutado por Jest antes de cada test y por lo tanto no es necesario añadir los imports para cada archivo de testeo.

Por ultimo necesitas decirle a Jest donde encontrar este archivo. Abre tu `jest.config.js` y añade esta entrada en el pie,después de 'setupFiles':

```js:title=jest.config.js
module.exports = {
  setupFilesAfterEnv: ["<rootDir>/setup-test-env.js"],
}
```

## Uso

Vamos a crear un pequeño ejemplo de test usando la nueva librería añadida. Si aún no lo has hecho lee la [guía de testeo unitario](/docs/unit-testing) — esencialmente ahora usarás `@testing-library/react` en vez de `react-test-renderer`. Hay un montón de opciones cuando se trata de selectores, aquí este ejemplo escoge `getByTestId`. También utiliza `toHaveTextContent` desde `jest-dom`

```js
import React from "react"
import { render } from "@testing-library/react"

// tienes que escribir data-testid
const Title = () => <h1 data-testid="hero-title">¡Gatsby es increible!</h1>

test("Displays the correct title", () => {
  const { getByTestId } = render(<Title />)
  // _Assertion_ (Afirmación)
  expect(getByTestId("hero-title")).toHaveTextContent("¡Gatsby es increible!")
  // --> El test será valido
})
```
