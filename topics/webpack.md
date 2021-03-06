Webpack is a bundler, which combines many javascript files into a single bundle file.

It also uglifies (shortens identifier names) and minifies (gets rid of whitespace) the code.

```bash
sudo npm install -g webpack-cli
```

The `webpack.config.js` configuration file can be generated by answering questions.  

```bash
webpack-cli init
```
Example :
1. Will your application have multiple bundles? **No**
2. Which module will be the first to enter the application? [example: './src/index.js'] **./src/index.js**
3. Which folder will your generated bundles be in? [default: dist] **Enter**
4. Are you going to use this in production? **No**
5. Will you be using ES2015 (ES6)? **Yes**
6. Will you use one of the below CSS solutions? **No**
7. Name your `webpack.[name].js`? [default: 'config'] **Enter**

This will install:
- webpack-cli
- uglifyjs-webpack-plugin
- babel-core
- babel-loder
- babel-preset-env
- webpack

It will also generate the `webpack.config.js` file:
```javascript
const webpack = require("webpack");
const path = require("path");

const UglifyjsJSPlugin = require("uglifyjs-webpack-plugin");

module.exports = {
    entry: './src/index.js',
    output: {
        filename: '[name].bundle.js',
        path: path.resolve(__dirname, dist)
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel-loader',
                options: {
                    presets: ['env'] 
                }
            }
        ]
    },
    plugins: [new UglifyJSPlugin()]
};
```
We can add this in `package.json` watch for changes and rebuild:
```json
{
    "scripts": {
        "build": "webpack -w"
    }
}
```