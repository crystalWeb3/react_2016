# A React Journey
## A tour of the latest trends in the React ecosystem

### TOC

* Webpack
  * CSS Modules
  * ES2015 / Babel
* React
* Redux
  * Mobx
* Enzyme


# Webpack
v1.1.x -> https://webpack.github.io/
v2 -> https://webpack.github.io/docs/roadmap.html

good tutorial -> http://www.pro-react.com/materials/appendixA/


## Loaders

* test:  A regular expression that matches the file extensions that should run through this loader (Required).
* loader:  The name of the loader (Required).
* include / exclude:   Optional setting to manually set which folders and files the loader should explicitly add or ignore.
* query:  The query setting can be used to pass Additional options to the loader.

```
loaders: [
  { test: /\.css$/, loader: "style!css" },
  {
    test: /\.js$/,
    exclude: /node_modules/,
    loader: 'babel',
    query: {
      presets: ['es2015','react']
    }
  }
]
```

The exclamation point `style!css` can be used in a loader configuration to chain different loaders to the same file types.

## Plugins

* ExtractTextPlugin
  `var ExtractTextPlugin = require('extract-text-webpack-plugin');`
  `{ test: /\.css$/, loader: ExtractTextPlugin.extract('style-loader', 'css-loader?modules&importLoaders=1&localIdentName=[name]__[local]___[hash:base64:5]!postcss-loader') },`
  `plugins: [new ExtractTextPlugin('style.css')]`
* HtmlWebpackPlugin
  ```
  var HtmlWebpackPlugin = require('html-webpack-plugin');

  ...

  plugins: [
    new HtmlWebpackPlugin({
      template: __dirname + "/app/index.tmpl.html"
    })
  ],
  ```
## CSS Modules

```
{
  test: /\.css$/,
  loader: 'style!css?modules'
}
```
or better:
```
{
  test: /\.css$/,
  loaders: [
    'style-loader',
    'css-loader?modules&sourceMap&importLoaders=1&localIdentName=[name]__[local]___[hash:base64:5]',
  ]
}
```

Probably one of the best intros into css-modules i've seen: https://css-modules.github.io/webpack-demo/
[github](https://github.com/css-modules/webpack-demo)


The real trick: **Atomic CSS Modules**
https://medium.com/yplan-eng/atomic-css-modules-cb44d5993b27#.to9dsgs6a

## ES2015 / babel
###class
>Today, we're happy to release React v0.13!  
The most notable new feature is support for ES6 classes, which allows developers to have more flexibility when writing components. Our eventual goal is for ES6 classes to replace React.createClass completely, but until we have a replacement for current mixin use cases and support for class property initializers in the language, we don't plan to deprecate React.createClass.

```
import React from 'react';

class MyComponent extends React.Component {
  constructor() {
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    console.log('hello world');
  }
  render() {
    return (
      <button onClick={this.handleClick}>Say Hello</button>
    );
  }
}
Contacts.propTypes = {

};
Contacts.defaultProps = {

};

export default MyComponent;
```
### Arrow function
`() => console.log('Hi world!')`

```
handleClick = () => {
  console.log('hello world');
};
```

### Destructuring
```
var foo = ["one", "two", "three"];
var [one, two, three]; = foo;
console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"
```
Destructuring Props
```
const { foo, bar } = this.props
```
### Spread Operator
>The ... operator (or spread operator) is already supported for arrays in ES6. There is also an ECMAScript proposal for Object Rest and Spread Properties. We're taking advantage of these supported and developing standards in order to provide a cleaner syntax in JSX.

```
var component = <Component foo={x} bar={y} />;

var props = {};
props.foo = x;
props.bar = y;
var component = <Component {...props} />;
```

**Rest and Spread Properties ...**
```
var { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x; // 1
y; // 2
z; // { a: 3, b: 4 }
```
