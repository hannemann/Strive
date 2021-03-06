# STRIVE

PostCSS Magento 2 system.

## Requirements

1. [Magento 2 CE](https://magento.com/products/community-edition) installed
1. [NodeJS](http://nodejs.org/) (with npm package manager)
2. [GulpJS](https://github.com/gulpjs/gulp) `$ npm install -g gulp` (sudo may be needed for mac users)

## Installation

1. Install via Composer: `composer require trive/theme-frontend-strive` or clone this repository under Magento /app/design/frontend/Trive/blank folder & [StriveGulpTool](https://github.com/trive-digital/StriveGulpTool) inside Magento_root/strive-gulp folder.
2. `bin/magento setup:upgrade`
3. `bin/magento setup:static-content:deploy`
4. Install node_modules with `npm install` or `yarn` inside strive-gulp folder
5. Set up Gulp file paths inside gulpfile.

## Features & Usage

- Fast css compilation thanks to PostCSS
- PostCSS theme fallback / child theme support
- Small (as possible) set of PostCSS base styles and settings needed to get a working development system. Hey, it looks somehow like a Magento base theme, right? ;)
- [BrowserSync](https://www.browsersync.io/) - instant css injecting into browser & weinre support
- Theme static content is watched & transferred directly into pub/static via Gulp. No need to use Magento content deploy during development.
- Added gulp clean and deploy tasks. If there is a need, `gulp clean` will remove everything in `var/cache`, `var/generation`, `var/view_preprocessed` & `pub/static` folder (Except .htaccess, magento blank & magento luma theme) and `gulp deploy` will deploy Magento static content (short of `bin/magento setup:static-content:deploy`).

- PostCSS plugins used on Strive (check [npmjs](https://www.npmjs.com/) for usage):
- [postcss-import](https://www.npmjs.com/package/postcss-import) - PostCSS plugin to transform @import rules by inlining content.
- [postcss-simple-vars](https://www.npmjs.com/package/postcss-simple-vars) - PostCSS plugin for Sass-like variables
- [postcss-extend](https://www.npmjs.com/package/postcss-extend) - As close to cssnext @extend as possible for PostCSS
- [postcss-nested](https://www.npmjs.com/package/postcss-nested) - PostCSS plugin to unwrap nested rules like how Sass does it.
- [autoprefixer](https://www.npmjs.com/package/autoprefixer) - Parse CSS and add vendor prefixes to CSS rules using values from the Can I Use website
- [cssnano](https://www.npmjs.com/package/cssnano) - A modular minifier, built on top of the PostCSS ecosystem.
- [css-mqpacker](https://www.npmjs.com/package/css-mqpacker) - Pack same CSS media query rules into one media query rule.
- [postcss-mixins](https://www.npmjs.com/package/postcss-mixins) - PostCSS plugin for mixins
- [lost](https://www.npmjs.com/package/lost) - LostGrid is a powerful grid system built in PostCSS that works with any preprocessor and even vanilla CSS.
- [postcss-responsive-type](https://www.npmjs.com/package/postcss-responsive-type) - PostCSS plugin that adds responsive magic to font-size
- [postcss-custom-media](https://www.npmjs.com/package/postcss-custom-media) - PostCSS plugin to transform W3C CSS Custom Media Queries to more compatible CSS
- [postcss-color-function](https://www.npmjs.com/package/postcss-color-function) - PostCSS plugin to transform W3C CSS color function to more compatible CSS.

## Gulp

### Creating a child theme

Gulpfile paths.cssSrc would be 'app/design/fronted/Trive/theme-name' and paths.cssDest: 'pub/static/frontend/Trive/theme-name/'. Child theme will need to have styles.css and settings.css inside the same folder structure like Strive (web/src/preCSS/), so it'll be needed to copy those two files from Trive/blank to child theme.

### Override css files

'postcss-import' looks for imported css files inside Trive/theme-name and if it can't find them here, it'll look into Trive/blank. To override existing blank theme css file, add css file with same name and path in child theme. postcss-import will take it instead of Trive/blank css.

File override example: Trive/blank/web/src/preCSS/theme/icons.css -> Trive/theme-name/web/src/preCSS/theme/icons.css

### Gulp Tasks

- `gulp` - Default gulp task (runs 'css', 'static', 'watch' & 'browser-sync' tasks). It watches css, html, images & js files. Browser-sync injects css file into the browser. These files, if changed, are auto transferred from theme to pub/static folder, so deployment of Magento static content would not be needed. Gulp-watch package is added to gulpfile so newly added files are watched also. This means it's not needed to restart gulp task anymore.

- `gulp clean` - Removes everything in `var/cache`, `var/generation`, `var/view_preprocessed` & `pub/static` folder (Except .htaccess, magento blank & magento luma theme)

- `gulp deploy` - It's a short of `bin/magento setup:static-content:deploy`. There is no problem to use longer option either :)

## Demo

Working demo of Strive can be checked here: [http://strive.jakesharpdev.com/](http://strive.jakesharpdev.com/)
