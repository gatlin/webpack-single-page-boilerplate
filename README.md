# Webpack Single Page Boilerplate

A boilerplate for a single page app using [webpack][webpack_link]

[![Build
Status](https://travis-ci.org/nihey/webpack-single-page-boilerplate.svg)](https://travis-ci.org/nihey/webpack-single-page-boilerplate)
[![Dependency
Status](https://david-dm.org/nihey/webpack-single-page-boilerplate.png)](https://david-dm.org/nihey/webpack-single-page-boilerplate)

# Why should I use it

So far, this is the best way I found to build files like `index.html` into
[webpack][webpack_link]. This boilerplate handles Javascript, CSS and HTML
bundling using only [webpack][webpack_link].

# Usage

The general directory structure is:

```
├── assets/
│   └── image
│       └── favicon.png
├── config/
│   ├── default.json
│   └── production.json
├── index.html
├── package.json
├── plugins/
│   └── html-plugin.js
├── README.md
├── scripts/
│   └── index.js
├── styles/
│   └── index.less
└── webpack.config.js
```

- Your javascript entry point is `scripts/index.js`
- Your style entry point is `styles/index.less`
- The `plugins/html-plugin.js` file is better explained on the *About* section,
  with the `html-parser-plugin` plugin.

[`config`][config_link] node module is being used, this way you can define
your settings under config/{NODE_ENV}.json and build your project with
different settings for different environments. Just change your `NODE_ENV`
environment variable to build your project:

### Example

```
# Uses 'config/default.json'
$ npm run build
# Uses 'config/default.json' overwritten by 'config/production.json'
$ NODE_ENV=production npm run build
# Uses 'config/default.json' overwritten by 'config/staging.json'
$ NODE_ENV=staging npm run build
# Uses 'config/default.json' overwritten by 'config/anything.json'
$ NODE_ENV=anything npm run build
```

All config variables are available under the `Environment` global:

```json
# config/default.json
{
  "MY_BACKEND": "https://nihey.org"
}
```
```javascript
// => "https://nihey.org"
console.log(Environment.MY_BACKEND)
```

There's a hack to build HTML files, replacing the `src` and `href` tags related
to images into their corresponding file in `dist` directory. This way, a
`index.html` file that looks like this:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Sample App</title>
    <meta charset="utf-8"/>
    <link href="!assets/image/favicon.png" rel="icon"/>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <script src="script.js"></script>
  </body>
</html>
```

Becomes this:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Sample App</title>
    <meta charset="utf-8">
    <link href="84eafba88857e5fd2e85d63beaf3fb31.png" rel="icon">
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <script src="script.js"></script>
  </body>
</html>
```

Notice that the `favicon.png` file was replaced with
`84eafba88857e5fd2e85d63beaf3fb31.png`. [indexhtml-webpack-plugin](https://github.com/unbroken-dome/indexhtml-webpack-plugin)
parses your `index.html` content and properly replace it on your
`dist/index.html`.

# About

This boilerplate includes the following loaders:

  - `babel-loader`: Enable ES6 features.
  - `file-loader`: Call `require` for binary files.
  - `img-loader`: Optimize image compression.
  - `json-loader`: Call `require` for `json` files.
  - `less-loader`: Style your pages with [less](http://lesscss.org/).
  - `style-loader`: Add exports of a module as style to DOM.

It also includes the following plugins:

  - `indexhtml-webpack-plugin`: Parses your html files content and build them.
  - `extract-text-webpack-plugin`: Extract css text from bundled styles.
  - `html-parser-plugin`: Custom experimental plugin to enable html parsing
                          on webpack. It is used to emit a `index.html` file
                          along with it's images.

# License

This code is released under
[CC0](http://creativecommons.org/publicdomain/zero/1.0/) (Public Domain)

[webpack_link]: http://webpack.github.io/
[config_link]: https://www.npmjs.com/package/config
