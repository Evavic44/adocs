![banner](https://user-images.githubusercontent.com/62628408/201538130-a1008969-06ae-4aad-9ea0-b77384d6bac1.png)

# How to build modern docs with VitePress

::: info
Documentation is a crucial aspect of software development that is often neglected by developers due to the hassle of maintaining one, or even choosing the right tools to use. This is why it's important to use tools that simplify this process. In this tutorial, you'll learn how to build a complete docs site quickly by utilizing a modern tool called, VitePress.
:::

## Definition

[VitePress](https://vitepress.vuejs.org/) is a simple and performant static site generator built on top of [Vite](https://vitejs.dev) for creating docs in a matter of minutes. It is powered by [Vuejs](https://vuejs.org/), and Vite with built in customizable components. VitePress powers some popular documentation sites like Vuejs, [Vitest](https://vitest.dev/), [faker.js](https://fakerjs.dev/), and Vite itself.

## Prerequisites

To follow along with this tutorial, you need to have a basic understanding of the following:

- [Markdown](https://daringfireball.net/projects/markdown/) syntax
- Brief understanding of NPM and Vite

Here's a screenshot of what you'll be building at the end of this tutorial.

![final-works](https://user-images.githubusercontent.com/62628408/201538907-fe67b791-02c4-413c-ae3d-02635b53e20b.png)

## Step. 1: Create a new project

If you already have a folder created, you can skip this step to the next one if not, use the following command to create a project folder and move into the folder.

```bash
mkdir project-name
cd project-name
```

Next you need to initialize with your preferred package manager. I'll be using NPM for the rest of this guide.

```bash
npm init
// or use this command if you want to skip all the questions
npm init -y
```

If you used the first command, you'll be prompted with certain questions, complete them as appropriate. After a successful operation, you should have a package.json file in your root directory; This is where the VitePress dev dependency will be installed.

## Step. 2: Install VitePress

Next step is to add VitePress and Vue as dev dependencies to your project.

```bash
npm install vue vitepress --save-dev
// or
npm install -D vue vitepress
```

You've successfully installed VitePress and Vue and added it as a dev dependency. Now you can start creating creating your respective doc files, but before you do that, I believe it's essential to explain how VitePress works.

## How does VitePress work?

VitePress makes use of Markdown `.md` files for it's markup which is automatically converted into static HTML. In other for this to work, a special folder called `docs` is created in the root directory.

This folder behaves similar to the `pages` folder in NextJS, where any `.js` file created in the directory is automatically treated as a web page. In this case a file called `index.md` will be the treated as `index.html` and serve as the root of your docs template.

Now you understand how that works, you can now create your respective doc files.

## Step 3. Create respective files

You can create the docs folder and the index.md file manually, or you can do it with the terminal like a hacker.

```bash
mkdir docs && echo '# Hello VitePress' > docs/index.md
```

This command is simply creating a folder called docs and adding an index.md file containing a h1 element that says, "Hello World".

![create respective files](https://user-images.githubusercontent.com/62628408/201539157-0b662a53-4aad-4ce5-b22c-228aa618d7b8.png)

With this, you can boot up your dev environment to see what has been created so far.

## Step 4: Boot up dev environment

In other to run your docs locally, you need to add the following scripts inside the package.json file. Simply copy the code below and replace it with the "script" object.

```js
// package.json
"scripts": {
    "docs:dev": "vitepress dev docs",
    "docs:build": "vitepress build docs",
    "docs:serve": "vitepress serve docs"
  },
```

Finally, the documentation site can be served on a local server by running the command below:

```bash
npm run docs:dev
```

This will start a hot-reloading development server at `http://localhost:5173`, and you can visit it to see your docs site.

### Output

![boot-dev-server](https://user-images.githubusercontent.com/62628408/201539308-bfc07160-bac2-4e91-ae90-46f9f3acd3cc.png)

All you had to do was add the markup and VitePress handled the looks from it's template engine. In the next session, you'll learn how you can customize the docs to fit your needs.

## How to customize your docs

First create a `.vitepress` folder inside the docs directory you created earlier on. This is where all VitePress-specific files will be placed. Inside this new directory, you need a `config.js` file. Again, you can use the terminal command as a hacker.

```bash
mkdir .vitepress && touch .vitepress/config.js
```

To test this config file, you can start by changing the meta title and description of your docs site. Copy this markup and paste into the `config.j`s file.

```js
// .vitepress/config.js
export default {
  title: "Adocs",
  description: "An awesome docs template built by me",
};
```

If you check the dev tools, you should see the changes in the meta title and description.

![title-and-description](https://user-images.githubusercontent.com/62628408/201539383-8b05db4c-dc00-4919-8bbc-f29cc77b2a00.png)

## Title and Logo

In other to change the logo title and add an image, copy the markup below and paste it into a new object called `themeConfig` inside the same `config.js` file. This will overwrite the current title and add a logo your docs site.

```js
// config.js
export default {
  themeConfig: {
    logo: "/logo.svg",
    siteTitle: "Adocs",
  },
};
```

For the image source, you can pass in an image URL or specify the path to a local image. To do it locally, make sure you place the image within the `public` directory.

### Output

![logo-and-title](https://user-images.githubusercontent.com/62628408/201539442-123b92cc-3c59-423d-a183-280ab8eb23be.png)

::: warning
Note: files in the public directory are served at the root path.
So instead of `../public/logo.svg`, just use `/logo.svg`.
:::

## Navbar

Customizing the `Navbar` is a pretty straightforward process as well. Inside your `themeConfig` file, paste the markup below. Here we have an object that contains two properties. The anchor text `text`, and the path, `link` defines the URL path.

```js
// .vitepress/config.js
{
  // ...
   nav: [
    { text: "About", link: "/about" },
    { text: "Contact", link: "/contact" },
    { text: "Guide", link: "/guide" },
    { text: "Configs", link: "/configs" },
    { text: "Changelog", link: "https://github.com/Evavic44" },
  ],
  // ...
}
```

Essentially navigating to `http://localhost:5173/about` should take you to an about page(though we haven't created that yet).

### Output

![navbar](https://user-images.githubusercontent.com/62628408/201539594-8e8f1d80-19dc-4335-b82b-fee5a23a5d30.png)

Navigation links can also be dropdown menus too. To add one, simply replace any of the links property with the items object which contains an array of links.

```js
// .vitepress/config.js
{
  text: "Changelog",
  items: [
   { text: "v0.0.1", link: "/item-1" },
   { text: "v0.0.2", link: "/item-2" },
   { text: "v0.0.3", link: "/item-3" },
  ],
},
```

Now changelog will become a dropdown menu with the respective links you pass inside.

### Output

![dropdown-menu](https://user-images.githubusercontent.com/62628408/201539670-330a0e0f-ed81-46b0-87cf-0d2b0b0c387b.png)

## Social Icons

Navigation menus usually have social icons visitors can use to visit your social platforms. To add that, define a new object called socialLinks inside themeConfig and simply pass in the social icon and the link you want it to navigate to.

```js
// .vitepress/config.js
socialLinks: [
  { icon: "github", link: "https://github.com/Evavic44/adocs" },
  { icon: "twitter", link: "https://twitter.com/victorekea" },
  { icon: "discord", link: "", target: "_blank" },
];
```

By default only 7 popular icons are provided. If you want to add a custom icon, use the SVG property to define an svg image.

```js
}
  "discord"
  "facebook"
  "github"
  "instagram"
  "linkedin"
  "slack"
  "twitter"
  "youtube"
  { svg: string };
{
```

::: warning
For the SVG icon, make sure you add the role="img" property, this allows the string convert it properly.
:::

![navbar-2](https://user-images.githubusercontent.com/62628408/201539773-a50280b7-91d4-4d4a-9ba7-a5c227fb9742.png)

## Sidebar

VitePress also comes with built-in components like sidebar menus. To add a sidebar, create an object called sidebar and inside we add nested objects that takes in three values; the nested title, collapsible functionality (Default is set to true) and the nested links.

```js
// .vitepress/config.js
sidebar: [
    {
      text: "Section A",
      collapsible: true,
      items: [
        { text: "Introduction", link: "/introduction" },
        { text: "Getting Started", link: "/getting-started" },
      ],
    },
    {
      text: "Section B",
      collapsible: false,
      items: [
        { text: "Introduction", link: "/introduction" },
        { text: "Getting Started", link: "/getting-started" },
      ],
    },
    {
      text: "Section C",
      collapsible: true,
      items: [
        { text: "Introduction", link: "/introduction" },
        { text: "Getting Started", link: "/getting-started" },
      ],
    },
  ],
```

By adding collapsible: "true" to the sidebar object, it shows a toggle button to hide/show each section. You can create as much sections as you want.

### Output

![sidebar-2](https://user-images.githubusercontent.com/62628408/201539859-92dffaf2-8886-4b11-86de-dd4847632536.png)

You can see section B is not collapsible and we have that aesthetic next page button on the bottom of the page.

## Page Routing

As explained earlier, VitePress automatically converts every `.md` file inside the root of the docs directory to static html that can be accessed in the address bar. For instance the `index.md` is converted to `index.html`, and `about.md`, about.html and so on.

Since you've created your nav links and pointed them to their respective URLs, you can access these pages easily by creating them.

```
docs/
├── .vitepress/
│   └── config.js
├── public/
│   └── logo.svg
├── about.md
├── contact.md
├── guide.md
├── configs.md
└── get-started.md
```

Create these files inside your docs folder and add a simple markup inside them just to see how this works. This page is basic markdown so all your markdown syntax like links, code blocks, headings, etc works here.

Just for testing purposes, copy this markdown content and paste it inside any of the `.md` file you just created.

```md
# About

Welcome to the about page.

This markdown supports html elements like the `p` tag coupled with inline styles

<p style="color: #ff7340; border: 1px solid rgba(255, 135, 23, 0.25); border-radius:5px; padding: 1rem;">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s.</p>

Even satire code snippets with syntax highlighting are also supported. 😅

const lang = prompt("What is your favorite programming language?");

(lang === "JavaScript") | (lang === "javascript") | (lang === "js")
? alert("JavaScript to the world! 🚀🟡")
: alert(`We don't permit such languages here 💩`);

Of course, images are not left out.

<img src="/logo.svg" alt="adocs logo">
```

### Output

![page-routing](https://user-images.githubusercontent.com/62628408/201539985-9308aaff-e98b-44e0-ad48-e990e788fd12.gif)

Great! You've set-up the docs, added a navigation menu with dropdown feature, added a sidebar, and customized the links to navigate to different pages. Next up, let's work on the home page.

## Customizing the home page.

Just like every other components, VitePress provides us with markup for building the home page. I've broken it down into three parts: Hero, features, and footer section.

## Hero Section

First, we'll start with the hero section. Replace the Hello World text in the `index.md` page with the following markup.

```bash
# docs/index.md
---
layout: home

hero:
  name: Adocs
  text: Static docs template built with VitePress.
  image:
    src: /logo-big.svg
    alt: Adocs logo
  tagline: A free to use template for creating docs for your projects
  actions:
    - theme: brand
      text: Get Started
      link: /get-started
    - theme: alt
      text: View on GitHub
      link: https://github.com/evavic44/adocs-template
---
```

## Features Section

Additionally, you can also add a features section after the hero section. Simply paste the code below under the hero objects.

```bash
# /docs/index.md
---
link: https://github.com/evavic44/adocs-template

features:
  - icon: ⚡️
    title: Adocs, The DX that can't be beat
    details: Lorem ipsum...
  - icon: 🎉
    title: Power of Vue meets Markdown
    details: Lorem ipsum...
  - icon: 🔥
    title: Simple and minimal, always
    details: Lorem ipsum...
  - icon: 🎀
    title: Stylish and cool
    details: Lorem ipsum...
---
```

### Output

![hero-redesign](https://user-images.githubusercontent.com/62628408/201540116-6546ba1f-dc43-4490-a6e5-b513eaf3ced6.png)

## Footer

You can add a footer message on the bottom of the page but this will only show up in the home page.

::: warning
The footer will not be displayed when the SideBar is visible.
To add the footer component, go to the `config.js file` and paste the markup inside the `themeConfig` object
:::

```js
// .vitepress/config.js
 footer: {
   message: "Released under the MIT License.",
   copyright: "Copyright © 2022-present Adocs",
 },
```

### Output

![footer](https://user-images.githubusercontent.com/62628408/201540337-4472a86e-f5cd-42d4-b40d-da1199148d2d.png)

Aside from the markup, you can also customize the components using custom CSS to change things like fonts family, colors, layout, ETC.

## Custom CSS

The default theme CSS is customized by overriding root level CSS variables. If you want, you can check out the full list of [css variables customizable](https://github.com/vuejs/vitepress/blob/main/src/client/theme-default/styles/vars.css).

To do get started, create a `.vitepress/theme directory`, and inside this theme folder, add an `index.js` and `custom.css` file. If you've been following along, you can use the terminal command below to do this quickly.

```bash
mkdir docs/.vitepress/theme && touch docs/.vitepress/theme/index.js && touch docs/.vitepress/theme/custom.css
```

If you ran into any issues with the terminal command, just create the files manually and move on to the next step.

Here's an overview of the folder structure.

```bash
docs/
├── .vitepress/
│   ├── config.js
│   └── theme/
│       ├── index.js
│       └── custom.css
├── public/
│   └── logo.svg
├── about.md
├── contact.md
├── guide.md
├── configs.md
└── get-started.md
```

After creating these files, inside the `.vitepress/theme/index.js file`, paste the import commands.

```js
// .vitepress/theme/index.js
import DefaultTheme from "vitepress/theme";
import "./custom.css";

export default DefaultTheme;
```

### Color Theme

The colors are controlled by the CSS variables. You can simply replace them with any colors you want.

::: tip
This color has a provision for both light and dark mode. So make sure you change them accordingly.
:::

Here's an example of my custom colors

```css
/* .vitepress/theme/custom.css */

:root {
  --vp-c-brand: rgb(255, 115, 64);
  --vp-c-brand-light: rgb(255, 87, 25);
  --vp-c-brand-lighter: rgb(255, 115, 64);
  --vp-c-brand-dark: #ff622d;
  --vp-c-brand-darker: rgb(226, 60, 0);

  --vp-c-sponsor: #fd1d7c;
}
```

If you don't see the effects immediately, try ending the server and starting it again.

Aside from the color themes, you can also override other things like, font family, typography, layout, breakpoints, etc.

## Fonts

[Google fonts](https://fonts.google.com/) can be imported inside the CSS file to override the default font family.

```css
@import url(https://fonts.googleapis.com/css?family=Space+Mono:regular,italic,700,700italic);
@import url(https://fonts.googleapis.com/css?family=Space+Grotesk:regular,italic,700,700italic);

:root {
  --vp-c-brand: #ff7340;
  --vp-c-brand-light: #ff5719;
  --vp-c-brand-lighter: #ff7340;
  --vp-c-brand-lighter: rgba(255, 135, 23, 0.25);
  --vp-c-brand-dark: #ff622d;
  --vp-c-brand-darker: #e23c00;

  --vp-c-sponsor: #fd1d7c;

  /* Typography */
  --vp-font-family-base: "Space Grotesk", "Inter var experimental", "Inter var",
    -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell,
    "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;

  /* Code Snippet font */
  --vp-font-family-mono: "Space Mono", Menlo, Monaco, Consolas, "Courier New",
    monospace;
}
```

With the `--vp-font-family-base` variable you can change the main font and `--vp-font-family-mono,` the font for code snippets.

### Output

![banner](https://user-images.githubusercontent.com/62628408/201538130-a1008969-06ae-4aad-9ea0-b77384d6bac1.png)

You've successfully customized the theme and changed the font family using CSS. Though there's more you can do in regards to styling, but at this point, I'm sure it's clearer how you can customize your docs with CSS. Let's discuss hosting in the next section.

## Hosting

You can publish or host your docs site when you're done to different platforms like: [Netlify](https://netlify.com/), [Vercel](https://vercel.com), [AWS Amplify](https://aws.amazon.com/amplify/), etc.

First, run the build command

```bash
npm run docs:build
```

This should create a new dist folder that contains all the static files of your docs. In your hosting service, add these commands to their respective fields.
Build command: npm run docs:build
Output directory: docs/.vitepress/dist

This should create a new `dist` folder that contains all the static files of your docs. In your hosting service, add these commands to their respective fields.

- Build command: `npm run docs:build`
- Output directory: `docs/.vitepress/dist`

![deploy-settings-vercel](https://user-images.githubusercontent.com/62628408/201540859-095ea3c0-5d97-4eb4-98a5-2601149d96ed.png)

After editing the settings, save, and deploy.

## Conclusion

In this tutorial, you've set-up a full-fledged documentation site and customized it using CSS and VitePress built-in components. However, this tutorial only covers a fragment of what is possible with VitePress, to learn more, check out the VitePress docs.

## Resources

- [Live Demo](https://adocs.vercel.app)
- [GitHub Repo](https://github.com/Evavic44/adocs)

<hr>

If you are an open source ardent like myself or you enjoy hearing about such cool projects, do follow me on my socials so you don't miss my next post. Cheers. 🍷

[GitHub](https://github.com/evavic44) [Twitter](https://twitter/.com/victorekea) [Blog](https://eke.hashnode.dev) [Portfolio](https://victoreke.com)
