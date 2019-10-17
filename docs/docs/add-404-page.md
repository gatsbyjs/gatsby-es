---
title: "Añadiendo una página 404"
---

Para crear una página 404, cree una pagina cuya ruta cumpla con la expresión regular
`^\/?404\/?$` (`/404/`, `/404`, `404/` o `404`). Lo más frecuente es crear un componente página de React en 
`src/pages/404.js`.

Gatsby se asegura de que la página 404 es construida como `404.html` ya que muchas plataformas de hospedaje
de sitios estáticos usan esta por defecto como su página de error 404. Si esta alojando su 
web de otra forma, necesitará configurar una regla personalizada que sirva este fichero ante 
errores 404.

Debido a que Gatsby crea esta página para usted por defecto, no hay necesidad de configurarla 
en el fichero `gatsby-node.js`.

Cuando se desarrolla usando `gatsby develop`, Gatsby utiliza una página 404 por defecto 
que sobreescribe la página 404 personalizada. No obstante, usted puede seguir previsualizando su página 404 
haciendo click en "Previsualizar página 404 personalizada", para verificar que esta funcionando 
como debería. Esto es útil cuando está desarrollando, ya que de esta manera puede ver todas las páginas disponibles.

La captura a continuación muestra la página 404 que Gatsby crea por defecto.
Además, lista todas las páginas disponibles en su sitio. Haciendo click en el botón "Previsualizar página 404 
personalizada" le permitirá ver la página 404 que ha creado.
![Página 404 por defecto de Gatsby](images/gatsby-default-404.png)

La captura a continuación, muestra una página 404 personalizada.
![Página 404 personalizada de Gatsby](images/gatsby-custom-404.png)
