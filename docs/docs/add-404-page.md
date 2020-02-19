---
title: "Añadiendo una página 404"
---

<<<<<<< HEAD
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
=======
To create a 404 page create a page whose path matches the regex `^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`). Most often you'll want to create a React component page at `src/pages/404.js`.

Gatsby ensures that your 404 page is built as `404.html` as many static hosting platforms default to using this as your 404 error page. If you're hosting your site another way you'll need to set up a custom rule to serve this file for 404 errors.

Because Gatsby creates this page for you by default, there is no need to configure it in your `gatsby-node.js` file.

When developing using `gatsby develop`, Gatsby uses a default 404 page that overrides your custom 404 page. However, you can still preview your 404 page by clicking "Preview custom 404 page" to verify that it's working as expected. This is useful when you're developing so that you can see all the available pages.

The screenshot below shows the default 404 page that Gatsby creates. It also lists out all the pages on your website. Clicking the "Preview custom 404 page" button will allow you to view the 404 page you created.
![Gatsby Default 404 Page](./images/gatsby-default-404.png)

The screenshot below shows the custom 404 page.
![Gatsby Custom 404 Page](./images/gatsby-custom-404.png)
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc
