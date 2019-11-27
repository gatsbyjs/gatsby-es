---
title: Glossary
disableTableOfContents: true
---

import HorizontalNavList from "../../www/src/components/horizontal-nav-list.js"

When you're new to Gatsby there can be a lot of words to learn. This glossary aims to give you a 10,000-foot overview of common terms and what they mean for Gatsby sites.

<HorizontalNavList
items={"ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("")}
slug={props.slug}
/>

## A

### AST

Abstract Syntax Tree: A tree representation of the source code that is found during a [compilation](#compiler) step between two languages. For example, [gatsby-transformer-remark](/packages/gatsby-transformer-remark/) will create an AST from [Markdown](#markdown) to describe a Markdown document in a tree structure using the [Remark](#remark) parser.

### API

Application Programming Interface: A method for one application to communicate with another. For example, a [source plugin](#source-plugin) will often use an API to get its data.

### Accessibility

The inclusive practice of removing barriers that prevent interaction with, or access to websites, by people with disabilities. When sites are correctly designed, developed and edited for accessibility, generally all users have equal access to information and functionality. Read about [Gatsby's Commitment to Accessibility](/blog/2019-04-18-gatsby-commitment-to-accessibility/).

## B

### Babel

A tool that lets you write the most modern [JavaScript](#javascript), and on [build](#build) it gets [compiled](#compiler) to code that most web browsers can understand.

### Backend

The behind the scenes that the [public](#public) do not see. This often refers to the control panel of your [CMS](#cms). These are often powered by server-side programming languages such as Node.js, PHP, Go, ASP.net, Ruby, or Java.

### Build

In Gatsby, this is the process of taking your code and content and packaging it into a website that can be hosted and accessed. Commonly referred to as _build time_. See also: [backend](#backend) and [server-side](#server-side).

## C

### Cache

A storage of information locally that might be used again, so computations and lookups can be retrieved faster from one place. Gatsby uses a cache to store information so it can build your site faster when you're developing without needing to do the same work twice.

### CLI

Command Line Interface: An application that runs on your computer through the [command line](#command-line) and interacted with your keyboard.

Gatsby has two command line interfaces. One, [`gatsby`](/docs/gatsby-cli/), for day-to-day development with Gatsby and another, [`gatsby-dev`](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions), for those who contribute to the Gatsby project.

### Client-side

Client-side refers to operations that are performed by the user's browser in a [client–server relationship](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) in a computer network. In Gatsby, this is important when [working with packages](/docs/using-client-side-only-packages/) that rely on objects in the [browser DOM](#dom), such as `window` or `navigator`. See also: [server-side](#server-side), [frontend](#frontend), and [backend](#backend).

### CMS

Content Management System: an application where you can manage your content and have it saved to a database or file for accessing later. Examples of Content Management Systems include WordPress, Drupal, Contentful, and Netlify CMS.

### Command Line

A text-based interface to run commands on your computer. The default Command Line applications for Mac and Windows are `Terminal` and `Command Prompt` respectively.

### Compiler

A compiler is a program that translates code written in one language to another language. For example [Gatsby](#gatsby) can compile [React](#react) applications into static [HTML](#html) files.

### Component

Components are independent and re-usable chunks of code powered by [React](#react) that, when combined, make up your website or app.

A component can include components within it. In fact, [pages](#page) and [templates](#template) are examples of components.

### Config

The configuration file, `gatsby-config.js` tells Gatsby information about your website. A common option set in config is your sites metadata that can power your SEO meta tags.

### CSS

[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) stands for Cascading Style Sheets, and it's a major part of the Web Platform with [HTML](#html) and [JavaScript](#javascript). CSS is a language for styling webpages designed to be highly backwards-compatible. As new features are rolled out to end-users, [CSS parsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#CSS_parsing) can safely ignore unsupported features and enhance with the properties they do support. CSS accomplishes this with its _cascading_ design, fundamental to styling with new techniques like [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_and_Progressive_Enhancement) while providing fallbacks for older browsers. Gatsby supports multiple [approaches to styling](/docs/styling/), including regular CSS files, CSS modules, and CSS-in-JS.

## D

### Data Source

Content and data's origin point, typically integrated into Gatsby with [source plugins](#source-plugin). A data source is often a [Headless CMS](#headless-cms), but it could also include Markdown, JSON, or YAML files.

### Database

A database is a structured collection of data or content. Often a [CMS](#cms) will save to a database using [backend technologies](#backend). They're often accessed in Gatsby via a [source plugin](#source-plugin)

### Decoupled

Decoupling describes the separation of different concerns. With [Gatsby](#gatsby) this most commonly means decoupling the [frontend](#frontend) from the [backend](#backend), like with [Decoupled Drupal](https://dri.es/how-to-decouple-drupal-in-2019) or [Headless WordPress](https://www.smashingmagazine.com/2018/10/headless-wordpress-decoupled/).

### Deploy

The process of [building](#build) your website or app and uploading onto a [hosting provider](#hosting).

### Development Environment

The [environment](#environment) when you're developing your code. It's accessed through the [CLI](#cli) using `gatsby develop`, and provides extra error reporting and things to help you debug before building for [production](#production-environment).

### DOM

The Document Object Model, commonly referred to as "the DOM", is a standard browser API that connects web pages to scripts or programming languages by representing the structure of an HTML document in memory. Developers commonly interact with the DOM through [HTML](#html) markup (written in [JSX](#jsx) in Gatsby), as well as both [React](https://reactjs.org/docs/react-dom.html) and [vanilla JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction#DOM_and_JavaScript) code. Another important aspect of utilizing the DOM to its full potential is writing [accessible](#accessibility) HTML markup to expose a page's structure to assistive technology.

## E

### ECMAScript

ECMAScript (often referred to as ES) is a specification for scripting languages. [JavaScript](#javascript) is an implementation of ECMAScript. Often developers will use [Babel](#babel) to [compile](#compiler) the latest ECMAScript code into more widely supported JavaScript.

### Environment

The environment that Gatsby runs in. For example, when you are writing your code you probably want as much debugging as possible, but that's undesirable on the live website or app. As such, Gatsby can change its behavior depending on the environment it's in.

Gatsby supports two environments by default, the [development environment](#development-environment) and the [production environment](#production-environment).

### Environment Variables

[Environment Variables](/docs/environment-variables/) allow you to customize the behavior of your app depending on its [environment](#environment). For instance, you may wish to get content from a staging CMS during development and connect to your production CMS when you [build](#build) your site. With environment variables you can set a different URL for each environment.

## F

### Filesystem

The way files are organized. With Gatsby, it means having files in the same place as your website's or app's code instead of pulling data from an external [source](#data-source). Common filesystem usage in Gatsby includes Markdown content, images, data files, and other assets.

### Frontend

The [public-facing](#public) interface for your website or app, delivered using web technologies: HTML, CSS, and JavaScript. For more insight into how the Web Platform brings these technologies together, check out this article on [How Browsers Work](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/).

## G

### Gatsby

Gatsby is a modern website framework that builds performance into every website or app by leveraging the latest web technologies such as [React](#react), [GraphQL](#graphql), and modern [JavaScript](#javascript). Gatsby makes it easy to create blazing fast, compelling web experiences without needing to become a performance expert.

### GraphQL

A [query](#query) language that allows you to pull data into your website or app. It’s the [interface that Gatsby uses](/docs/graphql/) for managing site data.

## H

### HTML

A markup language that every web browser is able to understand. It stands for Hypertext Markup Language. [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) gives your web content a universal informational structure, defining things like headings, paragraphs, and more. It is also key to providing an accessible website.

### Headless CMS

A [CMS](#cms) that only handles the [backend](#backend) content management instead of handling both the backend and [frontend](#frontend). This type of setup is also referred to as [Decoupled](#decoupled).

### Hosting

A hosting provider keeps a copy of your website or app and makes it accessible to [the public](#public). [Common hosting providers for Gatsby](/docs/deploying-and-hosting/) projects include Netlify, AWS, S3, Surge, Heroku, and more.

### Hot module replacement

A feature in use when you run `gatsby develop` that live updates your site on save of code in a text editor by automatically replacing modules, or chunks of code, in an open browser window.

### Hydration

Once a site has been [built](#build) by Gatsby and loaded in a web browser, [client-side](#client-side) JavaScript assets will download and turn the site into a full React application that can manipulate the [DOM](#dom). This process is often called re-hydration as it runs some of the same JavaScript code used to generate Gatsby pages, but this time with browser DOM APIs like `window` available.

## I

## J

### JAMStack

JAMStack refers to a modern web architecture using [JavaScript](#javascript), [APIs](#api), and ([HTML](#html)) markup. From [JAMStack.org](https://jamstack.org): "It’s a new way of building websites and apps that delivers better performance, higher security, lower cost of scaling, and a better developer experience."

### JavaScript

A programming language that helps us make the web dynamic and interactive. [JavaScript](https://developer.mozilla.org/en-US/docs/Web/Javascript) is a widely deployed web technology in browsers. It is also used on the server-side with [Node.js](#node). It is an implementation of the [ECMAScript](#ECMAScript) specification.

### JSX

JSX is an extension to JavaScript that allows developers to write HTML and custom components in the same piece of code. The [React team recommends](https://reactjs.org/docs/introducing-jsx.html) using it to describe what a [UI](#UI) should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript. Some important details to note are that because JSX uses JavaScript, some HTML attributes in your markup have to be swapped out to avoid reserved words in JavaScript (things like `htmlFor` and `className`).

## K

## L

### Linting

Linting is the process of running a program that will analyze code for potential errors. The Gatsby project uses [prettier](https://prettier.io/) to identify and fix common style issues. Another example of a linter commonly used in React projects is [eslint-jsx-plugin-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y), which checks for common [accessibility](#accessibility) issues in development.

## M

### MDX

Extends [Markdown](#markdown) to support [React](#react) [components](#component) within your content.

### Markdown

A way of writing HTML content with plain text, using special characters to denote content types such as hash symbols for [headings](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), and underscores and asterisks for text emphasis.

## N

### NPM

[Node](#node) [Package](#package) Manager. Allows you to install and update other packages that your project depends on. [Gatsby](#gatsby) and [React](#react) are examples of your project's dependencies. See also: [Yarn](#yarn).

### Node

Gatsby uses [data nodes](/docs/node-interface/) to represent a single piece of data. A [data source](#data-source) will create multiple nodes.

### Node.js

A program that lets you run [JavaScript](#javascript) on your computer. Gatsby is powered by Node.

## O

## P

### Package

A package usually describes a [JavaScript](#javascript) program that has additional information about how it should be distributed and used, such as its version number. [NPM](#npm) and [Yarn](#yarn) manages and installs the packages your project uses. [Gatsby](#gatsby) itself is a package.

### Page

An [HTML](#html) page.

This also often refers to [components](#component) that live in `/src/pages/` and are converted to pages by [Gatsby](#gatsby), as well as [pages created dynamically](/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) in your `gatsby-node.js` file.

### Plugin

Additional code that adds functionality to Gatsby that wasn't included out-of-the-box. Common [Gatsby plugins](/plugins/) include [source](#source-plugins) and [transformer](#transformer) plugins for pulling in and manipulating data, respectively.

### Production Environment

The [environment](#environment) for the [built](#build) website or app that users will experience when [deployed](#deploy). It can be accessed through the [CLI](#cli) using `gatsby build` or `gatsby serve`.

### Programmatically

Something that automatically happens based on your code and configuration. For example, you might [configure](#config) your project to create a [page](#page) for every blog post written, or read and display the current year as part of a copyright in your site footer.

### Progressive enhancement

Progressive enhancement is a strategy for the web that emphasizes core page content is loaded from a server before anything else, without [JavaScript](#javascript) as a requirement to load. This strategy then progressively adds more complex layers of presentation and features on top of the content as the end-user's browser/network connection allow. Gatsby's default approach to [building](#build) pages ahead-of-time means content will load first and enhance as scripts download and execute.

### Public

This usually refers to either a member of the public (as opposed to your team) or the folder `/public` in which your [built](#build) website or app is saved.

## Q

### Query

The process of requesting specific data from somewhere. With Gatsby you normally query with [GraphQL](#graphql).

## R

### React

A code library (written with [JavaScript](#javascript)) for building user interfaces. It’s the framework that [Gatsby](#gatsby) uses to build pages and structure content.

### Remark

A parser to translate [Markdown](#markdown) to other formats like [HTML](#html) or [React](#react) code.

### Runtime

Runtime is when a program is running (or being executable); it can refer to a few things. [Node.js](#nodejs) is a [server-side](#server-side) runtime that executes JavaScript code. [Client-side JavaScript](#client-side), on the other hand, refers to the browser runtime where traditional JavaScript code executes. Gatsby compiles your site at [build time](#build) and [rehydrates with a React runtime](#hydration) to provide a fast, interactive, and dynamic user experience.

### Routing

Routing is the mechanism for loading the correct content in a website or app based on a network request - usually a URL. For example, it allows for routing URLs like `/about-us` to the appropriate [page](#page), [template](#template), or [component](#component).

## S

### Schema

An exact representation of how data is stored in a system, such as tables and fields in a database or a JSON file structure. In Gatsby, the GraphQL schema expresses all queryable data - or data that components can ask about as part of Gatsby's data layer.

### Server-side

The server-side part of the [client-server relationship](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) refers to operations performed by a computer program which manages access to a centralized resource or service in a computer network. Gatsby uses the server-side technology [Node.js](#nodejs) to compile pages at build time, as opposed to serving them at [browser runtime](#runtime) with [client-side](#client-side) JavaScript. See also: [frontend](#frontend) and [backend](#backend).

### Source Code

Source code is your code that lives in `/src/` folder and makes up the unique aspects of your website or app. It is made up of [JavaScript](#javascript) and sometimes [CSS](#css) and other files.

The source code gets [built](#build) into the site the [public](#public) will see.

### Source Plugin

A [plugin](#plugin) that adds additional [data sources](#data-source) to Gatsby that can then be [queried](#query) by your [pages](#page) and [components](#component).

### Starter

A pre-configured Gatsby project that can be used as a starting point for your project. They can be discovered using the [Gatsby Starter Library](/starters/) and installed using the [Gatsby CLI](/docs/starters/).

### Static

Gatsby [builds](#build) static versions of your page that can be easily [hosted](#hosting). This is in contrast to dynamic systems in which each page is generated on-the-fly. Being static affords major performance gains because the work only needs to be done once per content or code change.

It also refers to the `/static` folder which is automatically copied into `/public` on each [build](#build) for files that don't need to be processed by Gatsby but do need to exist in [public](#public).

## T

### Template

A [component](#component) that is [programmatically](#programmatically) turned into a page by Gatsby.

### Theme

A Gatsby theme is like a WordPress theme that is composable (with other themes), extendable (with more logic), and replaceable ([shadowing](/blog/2019-04-29-component-shadowing/)). Gatsby themes can have any facet of a Gatsby app packaged inside of them, and can also offer any number of knobs to turn features on or off.

### Transformer

A [plugin](#plugin) that transforms one type of data to another. For example you might transform a spreadsheet into a [JavaScript](#javascript) array.

## U

### UI

A UI refers to a User Interface. In the field of human-computer interaction, a UI is a space where interactions between humans and machines occur. The goal of this interaction is to allow effective operation and control of the machine from the human end, while the machine simultaneously feeds back information that aids the user's decision-making process (such as error messages or notifications).

## V

## W

### Webpack

A [JavaScript](#javascript) application that Gatsby uses to bundle your website's code up. This happens automatically on [build](#build).

## X

## Y

### Yarn

A [package](#package) manager that some prefer to [NPM](#npm). It is also required for [developing Gatsby](/contributing/setting-up-your-local-dev-environment/#using-yarn).

## Z
