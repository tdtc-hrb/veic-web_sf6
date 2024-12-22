UI
====
- disables the Symfony UX Stimulus bridge
- Enabled Sass
- usage jquery

## Preparation
注意:  !!! at yarn V2 !!!
```
 如果没有 [yarn.lock](https://github.com/yarnpkg/berry/issues/2212) 文件, 在工程根目录新建一个空的.
```

- [install npm](https://tdtc-hrb.github.io/csdn/post/nodejs-ubuntu/)
- install yarn
```
sudo npm install --global yarn
```

### Sass
管理 JQuery && Bootstrap
```
yarn add sass --dev
yarn add sass-loader
```

- JQuery
```
yarn add jquery --dev
```
- Bootstrap
```
yarn add @popperjs/core --dev
yarn add bootstrap --dev
```

### update
- babel
- webpack

#### babel
```
yarn add @babel/core --dev
yarn add @babel/preset-env --dev
```
#### webpack
```
yarn add webpack --dev
yarn add webpack-cli --dev
yarn add webpack-notifier --dev
```
- webpack bridge
```
yarn add @symfony/webpack-encore --dev
```


## Asset Mapper
> 推荐在v8.4版本, 使用 AssetMapper
### [vendor - asset](https://symfony.com/blog/new-in-symfony-6-4-assetmapper-improvements#vendor-files-downloaded-locally)
- removed directory
```
assets/vendor
```
at .gitignore:
```
###> AssetMapper - Vendor Files Downloaded Locally ###
/assets/vendor/
###< AssetMapper - Vendor Files Downloaded Locally ###
```


## Enabled Sass
- webpack.config.js
```
// enables Sass/SCSS support
.enableSassLoader()
```

### User config
- app.scss
add app.scss file of assets/styles
```
@import "~bootstrap/scss/bootstrap";
```
- app.js
import it at app.js:
```
import './styles/app.scss';
```


## [usage jquery](https://symfony.com/doc/current/frontend/encore/legacy-applications.html#accessing-jquery-from-outside-of-webpack-javascript-files)
- defer
- symbol

### defer off
config/packages/webpack_encore.yaml:
```xml
webpack_encore:
    # The path where Encore is building the assets - i.e. Encore.setOutputPath()
    output_path: '%kernel.project_dir%/public/build'
    # If multiple builds are defined (as shown below), you can disable the default build:
    # output_path: false

    # Set attributes that will be rendered on all script and link tags
    script_attributes:
        defer: false
```
### symbol
> $

asset/app.js:
```
// require jQuery normally
const $ = require('jquery');

// create global $ and jQuery variables
global.$ = global.jQuery = $;
```
