## webpack学习笔记
#### 全局安装
```
npm install webpack -g
此时 Webpack 已经安装到了全局环境下，可以通过命令行 webpack -h 查看相关指令
```
#### 项目安装
```
npm install webpack --save-dev
npm info webpack 查看信息是否安装成功
```
#### tree-shaking
```
tree-shaking的原理是基于ES6的export关键字来扫描js文件，
没有export的就认为是无用的函数或者属性，打包的时候剔除掉
所以说与其说 tree-shaking 这个技术怎么了不起，
不如说是 ES6 module 的设计在模块静态分析上的种种考量值得赞赏 --尤雨溪
```
<a href="https://www.zhihu.com/question/41922432">参考</a>

#### 作用域提升
```
之前的webpack有一个权衡就是将各个模块bundle到一个独立的
闭包函数里面。这些独立的闭包函数会让js在浏览器中执行速度变
慢。就像Closure Compiler和 RollupJS的 将所有的模块‘提升’
或者链接到一个大的闭包里面，让你的代码在浏览器有更快的运行速度。
```
```
module.exports = {
  plugins: [
    new webpack.optimize.ModuleConcatenationPlugin()
  ]
};
```
<a href="https://zhuanlan.zhihu.com/p/27475789">参考</a>

#### Magic Comments
```
webpack2.0的时候我们介绍过引用语法（import()）支持动态引入的能力，但用户就表示比较关心它们不能像require.ensure那样给动态模块创建一个自有名字。

现在我们要给你介绍一个社区新词“magic comments”，可以让你传入一个模块名给你的import()，就像一个行内注释一样.详细可以看这里
通过使用注释，我们可以保存真实的加载信息，并且这也带来了你们喜爱的一个强大的模块命名功能。
```
```
import(/* webpackChunkName: "my-chunk-name" */ 'module');
```
<a href="https://zhuanlan.zhihu.com/p/27475789">参考</a>

#### Magic Comments