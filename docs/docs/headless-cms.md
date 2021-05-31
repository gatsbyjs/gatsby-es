---
title: ¿Qué es un _Headless CMS_ y cómo obtener contenidos de uno
overview: true
---

Un _headless CMS_ es un software de gestión de contenidos que permite a los escritores producir y organizar contenidos, mientras que provee a los desarrolladores con datos estructurados que pueden ser mostrados usando un sistema separado en el _frontend_ de un sitio web o una aplicación.

Un CMS monolítico tradicional, es responsable tanto de la administración del contenido del backend como de servir ese contenido a los usuarios finales. En contraste, un _headless CMS_ se desacopla de las preocupaciones del _frontend_, que libera a los desarrolladores para construir experiencias enriquecidas para los usuarios finales, utilizando la mejor tecnología disponible.

Muchos sistemas de gestión de contenidos (CMS) ahora soportan un modo _“headless”_ o “desacoplado”, que es perfecto para sitios con Gatsby.

Mediante el uso de [plugins fuente](/plugins/?=source), Gatsby tiene soporte para docenas de opciones de _headless CMS_, permitiendo a tu equipo de contenido la comodidad y familiaridad de su interfaz de administración preferida, y a tu equipo de desarrollo una experiencia de desarrollo y rendimiento mejoradas al usar Gatsby, GraphQL, y React para crear el _frontend_.

Las guías en esta sección explicarán el proceso de configuración de abastecimiento de contenidos de algunos de los _headless CMS_ más populares en uso actualmente.

<GuideList slug={props.slug} />

<!--
  El orden en esta sección se realiza mediante las descargas de plugins de Gatsby (/plugins/?=gatsby-source-) y el tamaño/adopción del proveedor del CMS.
-->

Aquí hay algunos recursos para guías, plugins, y _starters_ para sistemas CMS a los que puedes conectarte:

| CMS                                           | Guía                                                                             | Documentación del Plugin                                      | _Starter_ Oficial                                                   |
| --------------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------- |
| [Contentful](https://www.contentful.com/)     | [guía](/docs/sourcing-from-contentful/)                                          | [documentación](/packages/gatsby-source-contentful)           | [starter](/starters/contentful-userland/gatsby-contentful-starter/) |
| [NetlifyCMS](https://www.netlifycms.org/)     | [guía](/docs/sourcing-from-netlify-cms/)                                         | [documentación](/packages/gatsby-plugin-netlify-cms)          | [starter](/starters/netlify-templates/gatsby-starter-netlify-cms/)  |
| [WordPress](https://www.wordpress.com/)       | [guía](/docs/sourcing-from-wordpress/)                                           | [documentación](/packages/gatsby-source-wordpress)            |                                                                     |
| [Prismic](https://www.prismic.io/)            | [guía](/docs/sourcing-from-prismic/)                                             | [documentación](/packages/gatsby-source-prismic)              |                                                                     |
| [Strapi](https://strapi.io/)                  | [guía](/blog/2018-1-18-strapi-and-gatsby/)                                       | [documentación](/packages/gatsby-source-strapi)               |
| [DatoCMS](https://www.datocms.com/)           | [guía](https://www.gatsbyjs.com/guides/datocms/)                                 | [documentación](/packages/gatsby-source-datocms)              | [starter](/starters/datocms/gatsby-portfolio/)                      |
| [Sanity](https://www.sanity.io/)              | [guía](/docs/sourcing-from-sanity)                                               | [documentación](/packages/gatsby-source-sanity/)              |
| [Drupal](https://www.drupal.com/)             | [guía](/docs/sourcing-from-drupal/)                                              | [documentación](/packages/gatsby-source-drupal)               |                                                                     |
| [Shopify](https://www.shopify.com/)           |                                                                                  | [documentación](/packages/gatsby-source-shopify)              |                                                                     |
| [CosmicJS](https://cosmicjs.com/)             | [guía](/blog/2018-06-07-build-a-gatsby-blog-using-the-cosmic-js-source-plugin/) | [documentación](/packages/gatsby-source-cosmicjs)             | [starters](/starters/?s=cosmicjs&v=2)                               |
| [Contentstack](https://www.contentstack.com/) | [guía](/docs/sourcing-from-contentstack)                                         | [documentación](/packages/gatsby-source-contentstack)         | [starter](/starters/contentstack/gatsby-starter-contentstack/)      |
| [ButterCMS](https://buttercms.com/)           | [guía](/docs/sourcing-from-buttercms/)                                           | [documentación](/packages/gatsby-source-buttercms)            | [starter](/starters/ButterCMS/gatsby-starter-buttercms/)            |
| [Ghost](https://ghost.org/)                   | [guía](/docs/sourcing-from-ghost/)                                               | [documentación](/packages/gatsby-source-ghost/)               | [starter](/starters/TryGhost/gatsby-starter-ghost/)                 |
| [Kentico Cloud](https://kenticocloud.com/)    | [guía](/docs/sourcing-from-kentico-cloud)                                        | [documentación](/packages/gatsby-source-kentico-cloud)        | [starter](/starters/Kentico/gatsby-starter-kentico-cloud/)          |
| [Directus](https://directus.io/)              |                                                                                  | [documentación](/packages/gatsby-source-directus)             |
| [GraphCMS](https://graphcms.com/)             | [guía](/docs/sourcing-from-graphcms)                                             | [documentación](/packages/gatsby-source-graphql)              | [starter](/starters/GraphCMS/gatsby-graphcms-tailwindcss-example/)  |
| [Storyblok](https://www.storyblok.com/)       |                                                                                  | [documentación](/packages/gatsby-source-storyblok)            |
| [Cockpit](https://getcockpit.com/)            |                                                                                  | [documentación](/packages/gatsby-plugin-cockpit)              |
| [CraftCMS](https://craftcms.com/)             |                                                                                  | [documentación](/packages/gatsby-source-craftcms)             |
| [AgilityCMS](https://agilitycms.com/)         | [guía](/docs/sourcing-from-agilitycms/)                                          | [documentación](/packages/@agility/gatsby-source-agilitycms/) | [starter](/starters/agility/agility-gatsby-starter/)                |
| [Forestry](https://forestry.io/)              | [guía](/docs/sourcing-from-forestry/)                                           |                                                      |                                                                     |
| [Gentics Mesh](https://getmesh.io)            | [guía](/docs/sourcing-from-gentics-mesh)                                        |                                                      |                                                                     |
| [Seams-CMS](https://seams-cms.com/)           | [guía](/docs/sourcing-from-seams-cms)                                           |                                                      |                                                                     |

## Cómo añadir nuevas guías a esta sección

Si no ves tu CMS preferido en esta lista, puedes [escribir tú mismo una nueva guía](/contributing/how-to-contribute/) ó [abrir un _issue_ para solicitarla](https://github.com/gatsbyjs/gatsby/issues/new/choose).

También puedes [escribir tu propio plugin _source_](/docs/creating-a-source-plugin/) para integrar Gatsby con un CMS que no está en la lista.
