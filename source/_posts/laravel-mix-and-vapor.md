---
title: Mixing Laravel Mix with Vapor
date: 2017-01-17 3:17:15
tags:
- vapor
- laravel-mix
- front end
---

[Moving](https://ashokgelal.com/2017/01/16/laravel-to-vapor/) from a great framework like Laravel to Vapor is anything but easy. And as I was expecting, it didn't take me too long to realize this. Laravel is not only a solid, well-written, and well-documented framework but it also brings with it a handful of essential packages such as [Cashier](https://laravel.com/docs/5.3/billing), [Socialite](https://github.com/laravel/socialite), [Echo](https://laravel.com/docs/5.3/broadcasting), [Dusk](https://github.com/laravel/dusk) etc. These packages are officially supported and make your day to day job as a web developer much enjoyable and very productive.

The first thing I missed right away using Vapor was the lack of a good front end build tool for compiling assets such as JavaScripts and CSS. I'm sure there exists one but I didn't find any "officially promoted" one and nothing as good as [Laravel Elixir](https://laravel.com/docs/5.3/elixir), or it's next version - [Laravel Mix](https://github.com/JeffreyWay/laravel-mix).

Yes, I know there are many build tools such as [Gulp](http://gulpjs.com/), [Webpack](https://webpack.github.io/), [Grunt](http://gruntjs.com/), [Rollup](http://rollupjs.org/) etc. But, for better or worse, Laravel has spoiled me. I want to be more productive writing actual code and not spent hours fiddling with configurations.

Thankfully, Laravel Mix, despite its name, seems to work well with any other kind of frameworks including Vapor. There are few Laravel specific features such as the need for a function called `mix` if you need versioning but nothing that should block us from using it in our own Vapor project. In this post, I'll show you how to integrate Laravel Mix in your own Vapor project. ...

<!--more-->

### Initializing project and adding dependencies

1: Create a new Vapor project:

```swift
$ vapor new Hello
```

2: cd into `Hello` directory and initialize `npm` to create a new `package.json` file:

```bash
$ cd Hello && npm init -y
```

3: Let's install `laravel-mix` package:

```bash
$ npm install laravel-mix --save-dev
```

### Adding assets for compiling

We are now ready to compile our assets but first we need some assets. For this article, let's create one `.js` file and one `.scss` file:

1: Create `app.js` under `Resources/Assets/js` folder:

```bash
$ mkdir -p Resources/Assets/js && touch Resources/Assets/js/app.js
```

2: Open `app.js` file and add this:

```js
console.log('Mixing Laravel Mix with Vapor')
```

3: Create `app.scss` under `Resources/Assets/scss` folder:

```bash
$ mkdir -p Resources/Assets/scss && touch Resources/Assets/scss/app.scss
```

4: Open `app.scss` file and add this:

```css
body {
   background: red;
}
```

### Adding a mix file and Webpack commands

You need a `webpack.mix.js` file in the project's root folder. `webpack.mix.js` is like a master control for your assets. This is where you mix and remix your JavaScript files, CSS styles, copy fonts etc. Read [Laravel Mix documentation](https://github.com/JeffreyWay/laravel-mix/tree/master/docs) to learn more about this file.

1: Create a new file `webpack.mix.js` under project's root folder, open it and add the following:

```js
let mix = require('laravel-mix').mix
mix.js('Resources/Assets/js/app.js', 'Public/js')
   .sass('Resources/Assets/scss/app.scss', 'Public/css')
```

Here, we are saying that we want to compile `Resources/Assets/js/app.js` to `Public/js/app.js` file and `Resources/Assets/scss/app.scss` to `Public/css/app.css` file.

Now, we need to add some triggers to actually run compilation using this file. 

2: Open `package.json` file and add/ modify `scripts` object to include these npm scripts:

```js
  "scripts": {
    "webpack": "cross-env NODE_ENV=development webpack --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "dev": "cross-env NODE_ENV=development webpack --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "production": "cross-env NODE_ENV=production webpack --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  },
```

3: Now from the command line run:

```bash
$ npm run webpack
```

If everything goes well, you should see a **Compiled successfully** message.

![Success](/images/laravel-mix-run-webpack.png)

 
You should have two new files under your Public folder: `Public/js/app.js` and `Public/css/app.css` (Don't worry about `manifest.json` file for now). You can add these assets to your view files the way you would include any other .js or .css files.
   
If you want your assets to be compiled every time you make changes to one of your assets file, run this command:

```bash
$ npm run dev
```

When you are ready to publish your web app, you want your assets to be minified. In such case, you want to run:

```bash
$ npm run production
```

## Next

You can clone or fork the sample project for this tutorial on GitHub here: https://github.com/ashokgelal/laravel-mix-with-vapor

In a future post we'll cover other frontend awesomeness in a Vapor project such as using [Vue.js](https://vuejs.org/), using Hot Module Replacement with Webpack and Vue, versioning your assets for cache busting and some more.

Don't forget to bookmark this site and come back for more. If you want to say hi, I'm [@ashokgelal](https://twitter.com/ashokgelal) on Twitter.