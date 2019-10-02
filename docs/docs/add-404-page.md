---
title: "Agregar una página 404"
---

Para crear una página 404, cree una página cuya ruta coincida con la expresión regular
`^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`). La mayoría de las veces querrá crear una página de componentes React en
`src/pages/404.js`.

Gatsby asegura que su página 404 se construya como `404.html` tantos hosting estático
de forma predeterminada para usar esto como su página de error 404. Si estás alojando tu
de otra manera, deberá configurar una regla personalizada para servir este archivo para 404
errores.

Como Gatsby crea esta página de forma predeterminada, no es necesario configurar
en su `gatsby-node.js` file.

Al desarrollar usando `gatsby develop`, Gatsby usa una página 404 predeterminada que
anula la página 404 personalizada. Sin embargo, todavía puede obtener una vista previa de su página 404 por
haciendo clic en «Vista previa de la página 404 personalizada» para verificar que funciona como se esperaba. Esto es
útil cuando estás desarrollando para que puedas ver todas las páginas disponibles.

La siguiente captura de pantalla muestra la página 404 predeterminada que Gatsby crea.
También enumera todas las páginas de su sitio web. Al hacer clic en el botón "Vista previa 404 personalizada
página" le permitirá ver la página 404 que creó.
![Gatsby Default 404 Page](images/gatsby-default-404.png)

La siguiente captura de pantalla muestra la página 404 personalizada.
![Gatsby Custom 404 Page](images/gatsby-custom-404.png)
