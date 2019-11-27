---
title: Using the GraphQL Playground
---

## Intro

In this page we want to introduce you to an alternative to the current IDE for your GraphQL queries: [GraphQL Playground](https://github.com/prisma/graphql-playground).

## What is Prisma's GraphQL Playground?

GraphQL Playground is a way for you to interact with the data your sources and plugins add as schemas. You will be interacting with this data a lot and the Playground will help you greatly with exploring this data.

## Accessing the playground

To access this experimental feature utilizing GraphQL Playground with Gatsby, add `GATSBY_GRAPHQL_IDE` to your `develop` script in your `package.json`, like this:

```
"develop": "GATSBY_GRAPHQL_IDE=playground gatsby develop",
```

Use `npm run develop` instead of `gatsby develop` and access it when the development server is running on `https://localhost:8000/___graphql`

To still be able to use `gatsby develop` you would require the dotenv package to your gatsby-config.js file and add an [environment variable](/docs/environment-variables/) file, typically called `.env.development`. Finally, add `GATSBY_GRAPHQL_IDE=playground` to the `.env.development` file.

![An image pointing out where to find the GraphQl schema](images/playground-schema.png)
