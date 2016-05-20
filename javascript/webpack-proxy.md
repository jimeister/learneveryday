# Using webpack as proxy server

Webpack dev server can be used as a [proxy](https://webpack.github.io/docs/webpack-dev-server.html#proxy), but the configuration has to be within a `devServer` section. For example:

```
module.exports = {
  ...
  ...
  devServer: {
    hot: true,
    proxy: {
      '*': {
        target: 'http://localhost:8080'
      }
    }
  }
}
```
