# Setting-up-React-without-CRA

#### Prequisite

- Have Node installed
- Have knowledge of Javascript
- Have basic knowledge of React

Let's get started by creating a directory 

```
mkdir my-app
``` 
Next we navigate into the directory

```
cd my-app
``` 
We then create a package.json file by runing
```
npm init -y
```
Create a .gitignore file 
```
touch .gitignore
``` 
 Add node modules to the .gitignore file

*The -y flag tells npm to use all default config option while creating the package.json file

Next We need to install some dependencies:

install react and React dom

```
npm install react react-dom
``` 
Install webpack, webpack-dev-server and webpack-cli

```
npm i --save-dev webpack webpack-dev-server webpack-cli
``` 
Install @babel/core, babel-loader, @babel/preset-env, @babel/preset-react, html-webpack-plugin, css-loader, style-loader. html-webpack-plugin is a webpack plugin that makes it easy to create HTML files that serve webpack bundles.
```

npm install --save-dev @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli webpack-dev-server babel-loader css-loader style-loader html-webpack-plugin 
``` 
Create a webpack.config.js file in the root directory to configure webpack.

```
touch webpaack.config.js
``` 
Webpack is a module bundler. Its main purpose is to bundle JavaScript files for usage in a browser

In webpack.config.js require the path module and the html-webpack-plugin installed.

```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
``` 
In the webpack.config.js file specify an entry for the project 
```
module.exports = {
  entry: './src/index.js'
}
``` 
Specify the output path

```
output: {
  path: path.join(__dirname, '/dist'),
  filename: 'bundlefile.js'
}
``` 
At this point our webpack.config.js file should look like this 
```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.join(__dirname, '/dist'),
    filename: 'bundlefile.js'
  },
}
```
Specify the test files

```
module: {
rules : [
         {
          test: /\.js$/,
         }
        ]
},
``` 

Specify the Loader and exclude the node_modules
```
module: {
rules : [
         {
          test: /\.js$/,
          use: [ 'babel-loader'],
          exclude: /node_modules/,
         }
        ]
},
``` 

Create the src directory 

```
mkdir src
``` 
Navigate into the directory

```
cd src
``` 

The  Create the index.js and index.html files inside the src directory.

```
touch index.html index.js
``` 
In the index.html file, create a template html file and in its body, create a div with an id of  ‘App’

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>My React App</title>
  <meta name="viewport" content="width=device-width, initial-   scale=1">
  <link rel="stylesheet" type="text/css" media="screen" href="main.css" />
  <script src="main.js"></script>
</head>
<body>
  <div id="App"></div>
</body>
</html>
``` 
In the index.js file import React and React Dom. Create a class App that returns a div of 'hello world'.

```
import React from 'react';
import ReactDOM from 'react-dom';
class App extends React.Component{
    render(){
        return(
            <div>Hello World</div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('app'))

``` 

Add html-webpack-plugin to bundle the index.html file we created.

```
plugins: [
  new HtmlWebpackPlugin({
  template: './src/index.html'
  })
]
``` 
Your webpack.config.js file should look like this:

```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.join(__dirname, '/dist'),
    filename: 'bundlefile.js'
  },
module: {
rules : [
         {
          test: /\.js$/,
          use: [ 'babel-loader'],
          exclude: /node_modules/,
         }
        ]
},
  plugins: [
    new HtmlWebpackPlugin({
       template: './src/index.html'
    })
  ]
}
``` 
Babel is a JavaScript compiler and to Configure the application to use babel by creating a .babelrc file in the root directory of the project.

```
touch .babelrc
``` 
The .babelrc file is an object. In it, set the presets to work based on the environment of the application( test, development, production).
```
{
  "presets": [
    "@babel/preset-env",
    "@babel/react"
  ]
}
``` 
In package.json, write the start script:

```
"start": "webpack-dev-server --mode development --open",

``` 
Now when you run npm run start it will start the dev server and open your app in the browser.

To run the project:
```
npm run start
``` 
