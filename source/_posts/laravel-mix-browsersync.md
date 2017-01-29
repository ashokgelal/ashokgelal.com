---
title: Using Browsersync with Laravel Mix
date: 2017-01-29 9:22:15
tags:
- webpack
- laravel-mix
- browsersync
---

[Laravel Mix](https://github.com/JeffreyWay/laravel-mix) is basically a wrapper around Webpack now and comes with few scripts out-of-the-box. This is great and I like it a lot, esp. [Hot Module Replacement](https://github.com/JeffreyWay/laravel-mix/blob/master/docs/hot-module-replacement.md) part. But this also means we can no longer use old Laravel Elixir plugins. The one plugin that I really missed was the [Browsersync](https://github.com/JeffreyWay/laravel-elixir-browsersync-official) support.

At first, I thought I'd fine with it but as soon as I started working on a [real project](https://todayiread.online), I realized that the lack of auto-refreshing of browser made me less productive. After spending hours trying different things to make Browsersync work, I finally got it working and turns out it is actually very easy. Here are the steps:

1: Install npm dependencies:

```bash
$ npm browser-sync browser-sync-webpack-plugin webpack-dev-server  --save-dev
```

2: Open `webpack.mix.js` and append following code:

```js
const BrowserSyncPlugin = require('browser-sync-webpack-plugin')
mix.webpackConfig({
  plugins: [
    new BrowserSyncPlugin({
      open: 'external',
      host: 'todayiread.dev',
      proxy: 'todayiread.dev',
      files: ['resources/views/**/*.php', 'app/**/*.php', 'routes/**/*.php']
    })
```

That's it for the configuration!

3: To Webpack and then Browsersync your app:

```bash
$ npm run watch
```

Now, if you change any PHP files under app, resources/views, or routes folders, Browsersync will auto reload your browser. On the other hand, if you change any of your assets, Webpack will compile your assets first and then Browsersync will reload the browser. So long, F5 key!