---
title: "Creando Aplicaciones con Gatsby"
---

Gatsby es un _framework_ excelente para crear aplicaciones web. Puedes usar Gatsby para crear experiencias personalizas y de sesión con dos enfoques diferentes.

1.  páginas de aplicaciones "híbridas", y
2.  rutas solo para clientes y autenticación de usuarios

## Páginas de aplicaciones híbridas

Cuando un visitante llega a tu página Gatsby, el archivo HTML de la página se carga primero, después el paquete JavaScript; cuando tus componentes React se cargan en el navegador, pueden obtener y renderizar datos desde APIs.

> 💡 La [documentación de React](https://reactjs.org/docs/faq-ajax.html) tiene un gran y sencillo ejemplo demostrando este enfoque.

Algunos ejemplos en los que podrías aplicar esto:

- Un sitio de noticias con datos en vivo como resultados deportivos o el tiempo
- Un sitio de comercio electrónico con páginas de producto universales y páginas de categorías, pero también secciones de recomendaciones personalizadas

También puedes usar tus componentes React para crear widgets interactivos p.ej. permitir a un usuario realizar búsquedas o enviar formularios. Porque Gatsby es solo React, es fácil combinar modelos estáticos e interactivos/dinámicos para crear sitios web.

## Rutas solo para clientes y autenticación de usuarios

A menudo quieres crear un sitio con rutas exclusivas para clientes que están protegidas por autenticación. Para saber más sobre este enfoque, consulta la guía de referencia en [rutas y autenticación solo para clientes](/docs/client-only-routes-and-user-authentication/).
