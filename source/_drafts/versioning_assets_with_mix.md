---
title: Versioning Assets with Laravel Mix and Vapor Mix
date: 2017-01-18 20:25:25
tags:
- vapor
- laravel-mix
- front end
---

In the [previous tutorial][2], I showed you how you can use [Laravel-Mix](https://github.com/JeffreyWay/laravel-mix) to compile your front end assets. In this post, I'll show you how you can use Laravel Mix and a new Vapor package to compile, minify, and version your assets without breaking a sweat. ...

<!--more-->

### Minifying your assets:

As we saw in the previous tutorial, we have 3 *npm run* scripts at our disposal that we can use to compile our assets:

1: `npm run webpack` - to just compile the assets.

2: `npm run dev` - to continuously build the assets as you modify them.

3: `npm run production` - we didn't cover this but this is what you'd use to compile your assets for production. Among few other things, the most important task it performs is [minifying](https://www.maxcdn.com/one/visual-glossary/minification/) your assets.

### Versioning your assets:

As you know, browsers cache your assets to avoid downloading the same assets every time your load a page. But when you modify your assets, you want to force browsers to serve fresh copies. You can do this manually by adding a timestamp or a unique hash to your assets. If you use Laravel Mix, you can make it all automatic:

1: Open your `webpack.mix.js` file and call `.version()`. Your file should look like this:

```js
let mix = require('laravel-mix').mix
mix.js('Resources/Assets/js/app.js', 'Public/js')
   .sass('Resources/Assets/scss/app.scss', 'Public/css')
   .version()
```

2: Now from your terminal run:

```bash
$ npm run production
```

You will now see that it generated few hashed files. You can now refer to these files from your .html/.leaf file as follows:

```html
<link rel="stylesheet" href='/css/app.xxxx.css'>
...
<script src='/js/app.yyyy.js'></script>
```

where *xxxx* and *yyyy* are hashes of corresponding files.

### Dealing with dynamic hashed filenames:

The thing is, as you change a file, its hash gets changed as well. So you have to remember to update all your asset references every time you make a change.

I know, it's a pain to do that. What's even worse is that because files are only versioned in production, when you are developing, you have to remember to change them back to non-versioned filenames.

To deal with this I've created a package called [Vapor Mix][1]. This package comes with a leaf tag that allows you to load hashed asset within your *.leaf* view files without referring to the hash of the file. The above scripts would look like this using [Vapor Mix][1]:

```html
<link rel="stylesheet" href='#mix("/css/app.css")'>
...
<script src='#mix("/js/app.js")'></script>
```

You can learn more about [**Vapor Mix**][1] package on [it's GitHub repo][1].

## Next

Now that we have [Vapor Mix][1], we can do [Hot Module Replacement](https://webpack.github.io/docs/hot-module-replacement.html). But before we dive into it, we'll spend some time playing with [Vue.js](https://vuejs.org/) in a future post.

Don't forget to bookmark this site and come back for more. If you want to say hi, I'm [@ashokgelal](https://twitter.com/ashokgelal) on Twitter.

[1]: https://github.com/ashokgelal/vapor-mix
[2]: https://ashokgelal.com/2017/01/17/laravel-mix-and-vapor/
