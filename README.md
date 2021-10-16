1.SPA增加多页面入口的功能（访问路径：http://localhost:8080/test.html#!/index）；
主要配置：
01）webpack.base.conf.js
entry: {
  app: './src/main.js',
  test:'./src/test.js'
},
02）webpack.dev.conf.js
new HtmlWebpackPlugin({
  filename: 'test.html',
  template: 'test.html',
  chunks: ['test'],
  inject: true
})
03）webpack.prod.conf.js
new HtmlWebpackPlugin({
  filename: process.env.NODE_ENV === 'testing'
    ? 'test.html'
    : config.build.test,
  template: 'test.html',
  inject: true,
  minify: {
    removeComments: true,
    collapseWhitespace: true,
    removeAttributeQuotes: true
    // more options:
    // https://github.com/kangax/html-minifier#options-quick-reference
  },
  // necessary to consistently work with multiple chunks via CommonsChunkPlugin
  chunksSortMode: 'dependency'
}),
04)根目录，新增config.js
// see http://vuejs-templates.github.io/webpack for documentation.
var path = require('path')
module.exports = {
   build: {
		index: path.resolve(__dirname, 'dist/index.html'),
		test: path.resolve(__dirname, 'dist/test.html'),
		assetsRoot: path.resolve(__dirname, 'dist'),
		assetsSubDirectory: 'static',
		assetsPublicPath: '/',
		productionSourceMap: false
	},
	dev: {
		port: 8080,
		proxyTable: {}
	}
}
