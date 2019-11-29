---
title: Internal Data Bridge
---

> This documentation isn't up to date with the latest version of Gatsby.
>
> Outdated areas are:
>
> - should mention `siteMetaData` as an internal type
>
> You can help by making a PR to [update this documentation](https://github.com/gatsbyjs/gatsby/issues/14228).

The Internal Data Bridge is an internal Gatsby plugin located at [internal-plugins/internal-data-bridge](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby/src/internal-plugins/internal-data-bridge). Its purpose is to create nodes representing pages, plugins, and site config so that they can be introspected for arbitrary purposes. As of writing, the only usage of this is by the [gatsby-plugin-sitemap](/packages/gatsby-plugin-sitemap) which uses it to... yes you guessed it, create a site map of your site.

## Example usage

As a site developer, you can write queries to introspect your site's information. For example, to get a list of all Gatsby plugins that you're using:

```graphql
{
  allSitePlugin(limit: 10) {
    edges {
      node {
        name
      }
    }
  }
}
```

## Internal types

The internal data bridge creates 3 types of nodes that can be introspected.

### Site

This is a node that contains fields from your site's `gatsby-config.js`, as well as program information such as host and port for the local development server.

### SitePlugin

A Node for each plugin in your `gatsby-config.js` that contains the full contents of the plugin's `package.json`.

### SitePage

Internal Data Bridge implements [onCreatePage](/docs/node-apis/#onCreatePage) and creates a node of type `SitePage` that represents the created Page. Which allows you to introspect all pages created for your site.
