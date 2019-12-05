---
title: Obteniendo datos desde Contentful
---

## ¿Qué es Contentful? ¿Por qué elegirlo?

[Contentful](https://www.contentful.com/) es un _headless CMS_ que le permite
organizar su contenido en lo que podría llamarse "módulos", o pequeños pedazos de datos que pueden reorganizarse para que se vean bien en dispositivos móviles, tabletas, computadoras, dispositivos de realidad virtual (tal vez algún día?) y más.

En realidad, la forma en que Contentful maneja fragmentos de contenido significa que puede expulsar el contenido cuando se desarolle una nueva tecnología sin tener que rediseñar, reescribir, o repensar todo para un nuevo formato.

## Prerrequisitos

Esta guía assume que tiene un proyecto de Gatsby configurado. Si necesita configurar un proyecto, diríjase a la [Guía de Inicio Rápido](/docs/quick-start),luego regreze.

## Introducir datos y expulsarlos

Si tienes un archivo JSON con contenido, puedes colocarlo en Contentful usando [contentful-import](https://github.com/contentful/contentful-import). Si estás creando contendio nuevo, no necesita esto y simplemente crea contenido directamente en Contentful.

Si creas contenido directamente en Contentful, asegúrate de nombrar sus _fields_ de una manera que puedas recordar cuando crees consultas en _GraphQL_. Si usas GraphiQL, puedes sugerirle campos, pero esto sólo ayudará si los nombres del los campos son claros y memorables.

En cuanto a enviar datos a tu sitio, le sugerimos que use este fantástico plugin: [gatsby-source-contentful](https://www.npmjs.com/package/gatsby-source-contentful), para usarlo, necesitarías tener el `spaceId` y el `accessToken` provenientes de contentful.

## Instalación

```shell
npm install --save gatsby-source-contentful
```

## Cómo utilizar

### Con la API de _Delivery_

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-source-contentful`,
    options: {
      spaceId: `tu_space_id_agarralo_de_contentful`,
      accessToken: `tu_token_id_agarralo_de_contentful`
    }
  }
];
```

### Con la API de _Preview_

```javascript:title=gatsby-config.js
plugins: [
  {
    resolve: `gatsby-source-contentful`,
    options: {
      spaceId: `tu_space_id_agarralo_de_contentful`,
      accessToken: `tu_token_id_agarralo_de_contentful`,
      host: `preview.contentful.com`
    }
  }
];
```

## Ejemplos de sitios web con Gatsby + Contentful

El blog de Gatsby [tiene varios ejemplos de individuos y empresas](/blog/tags/contentful) que eligieron construir con Gatsby y Contentful.
