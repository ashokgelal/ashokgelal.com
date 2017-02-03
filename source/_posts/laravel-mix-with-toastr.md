---
title: Using toastr with Laravel Mix
date: 2017-02-02 21:19:15
tags:
- webpack
- laravel-mix
- toastr
---

I use [toastr]() for showing alerts in my web apps. Before it was as easy as adding a script tag and a link tag from CDNJS. But with Webpack and Laravel 5.4, this no longer works. Not just `toastr`, I've found that, at least in my experience, any libraries that depend on jQuery has the same issue. The only way I could make it work is through npm. It's a bit pain to npm every package, to be honest. ...

<!--more-->

Anyway, this is how I got to work toastr with my new Laravel 5.4 app:

1: Install toastr through npm:

```bash
$ npm install toastr --save-dev
``` 

2: Require it from `bootstrap.js` and make it available globally:

```js
window.toastr = require('toastr')
```

3: Import `toastr.scss` or `toastr.less` from one of your `app.scss` or `app.less` file:

```scss
@import "~toastr/toastr.scss";
```

That's it!

4: Now, to show a success toast from your `.js` or `.vue` file, do:

```js
toastr.success('toastr now works with Laravel 5.4+')
```

If you know how to use `toastr` with `Laravel Mix` without npm, please send me a tweet. I'm [@ashokgelal](https://twitter.com/ashokgelal) on Twitter.