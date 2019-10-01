---
título: "Agregar una página 404"
---

Para crear una página 404, cree una página cuya ruta coincida con la expresión regular
`^ \ /? 404 \ /? $` (`/ 404 /`, `/ 404`,` 404 / `o` 404`). La mayoría de las veces querrá crear una página de componente Reaccionar en
`src / pages / 404.js`.

Gatsby se asegura de que su página 404 esté construida como `404.html` como muchos hosting estáticos
plataformas por defecto para usar esto como su página de error 404. Si estás alojando tu
sitio de otra manera, tendrá que configurar una regla personalizada para servir este archivo para 404
errores

Debido a que Gatsby crea esta página para usted de manera predeterminada, no hay necesidad de configurar
en su archivo `gatsby-node.js`.

Al desarrollar usando `gatsby desarrollo`, Gatsby usa una página 404 predeterminada que
anula su página 404 personalizada. Sin embargo, aún puede obtener una vista previa de su página 404 por
haciendo clic en "Vista previa de página 404 personalizada" para verificar que funciona como se esperaba. Esto es
útil cuando se está desarrollando para poder ver todas las páginas disponibles.

La siguiente captura de pantalla muestra la página 404 predeterminada que crea Gatsby.
También enumera todas las páginas de su sitio web. Al hacer clic en "Vista previa personalizada 404
página "le permitirá ver la página 404 que creó.
! [Página predeterminada de Gatsby 404] (images / gatsby-default-404.png)

La captura de pantalla siguiente muestra la página 404 personalizada.
[Página Gatsby Custom 404] (images / gatsby-custom-404.png)