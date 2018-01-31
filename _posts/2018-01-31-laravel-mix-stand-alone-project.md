---
layout: post
title: Laravel Mix Stand-Alone Project
tags: Webpack
thumbnail: /assets/images/uploads/thumnail-laravel-mix.JPG
permalink: '/:year/:month/:day/:title'
---
```
mkdir my-app && cd my-app
npm init -y
npm install laravel-mix --save-dev
```

![Inizializando proyecto](/assets/images/uploads/mix-1.JPG)

For Linux you can use

```
cp -r node_modules/laravel-mix/setup/webpack.mix.js ./
```

Now for Windows

```
xcopy /F "C:\Users\Username\Desktop\Laravel-mix\node_modules/laravel-mix/setup/webpack.mix.js" C:\Users\Username\Desktop\Laravel-mix\
```

![Copiando webpack.mix.js](/assets/images/uploads/mix-2.JPG)

You should now have the following directory structure:

* `node_modules/`
* `package.json`
* `webpack.mix.js`

![Directory structure](/assets/images/uploads/mix-3.JPG)

Your file webpack.mix file

```
let mix = require('laravel-mix');

mix.js('src/app.js', 'dist')
   .sass('src/app.scss', 'dist')
   .setPublicPath('dist');
```

Take note of the source paths, and create the directory structure to match (or, of course, change them to your preferred structure). You're all set now. Compile everything down by running `node_modules/.bin/webpack` from the command line. You should now see:

* `dist/app.css`
* `dist/app.js`
* `dist/mix-manifest.json` (Your asset dump file, which we'll discuss later.)

Nice job! Now get to work on that project.

As a tip, consider adding the following NPM scripts to your `package.json` file, to speed up your workflow. Laravel installs will already include this.

These scripst only are for Mac or Linux

```
"scripts": {
    "dev": "NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch": "NODE_ENV=development node_modules/webpack/bin/webpack.js --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "hot": "NODE_ENV=development webpack-dev-server --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
    "production": "NODE_ENV=production node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  }
```

For Windows you could use 

```
"scripts": {
    "dev": "set NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch": "set NODE_ENV=development node_modules/webpack/bin/webpack.js --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "hot": "set NODE_ENV=development webpack-dev-server --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
    "production": "set NODE_ENV=production node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  }
```

Only add `set` before NODE_ENV

But my sripts are those

```
"scripts": {
    "dev": "webpack --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch": "webpack --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "hot": "webpack --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
    "production": "webpack --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  }
```

And webpack.mix file code

```
let mix = require('laravel-mix');mix.scripts(['src/assets/js/app.js',], 'dist/app.js').styles(['src/assets/css/app.css',], 'dist/app.css');
```
