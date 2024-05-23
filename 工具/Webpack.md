## 按装

1. 本地安装

   * 安装最新版或特定版

      ```
      npm install --save-dev webpack
      npm install --save-dev webpack@<version>
      ```

   * 使用`webpack v4+` 版本，还需安装CLI

      ```
      npm install webpack-cli
      ```

2. 全局安装

   * 通过npm安装方式，可以使用webpack在全局环境下可用

      ```
      npm install --global webpack
      ```

3. 初始化项目

   * 创建一个目录。初始化`npm`，安装`webpack-cil`（用于在命令行中运行`webpack`）:

      ```javascript
      mkdir webpack-demo//创建项目名称
      cd webpack-demo//进入项目
      npm init -y
      npm install webpack webpack-cli --save-dev
      ```

4. 更改npm镜像

   * 使用那个镜像，只需要 `npm config set registry +` 对应的镜像网址就好了

   * 淘宝镜像

      ```
       npm config set registry https://registry.npmmirror.com
      ```

5. 查看`webpack`版本号`npx webpack -v`

6. 打包

   * 不使用配置文件
   
      ```
      webpack src/index.js -o dist/index.js
      //将src下的文件打包到dist下
      ```
   
      * `{entery file}`：入口文件的路径，`src/index.js`
      * `{destination for bundled file}`：打包后存放的路径。
   
   * 使用配置文件
   
      ```
      webpack [--config webpack.config.js]
      ```

## 配置

1. 所有的配置写在配置文件中`webpack.config.js`，在项目文件下面，最高级

   ```js
   //处理当前文件目录
   const path = require('path');
   module.exports={
       //入口文件配置项
       entry:{
           main:''
       },
       //出口文件配置项
       output:{
           path:path.resolve(__dirname,''),
           filename:''
       },
       //模块：解读css，图片如何转换，压缩
       module:{},
       //插件，用于生产模板和各项功能
       plugins:{},
       //配置webpack开发服务功能
       devServer:{}
   }
   ```

   * **`path`**：Node.js Path模块
   * **`path.resolve`**：将文件转换为绝对路径
   * **`_dirname`**：Node.js中的全局变量，指当前文件所在的目录

## 入口、输出

**入口起点 (entry point)** 指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后， webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

默认值是 `./src/index.js` ，但你可以通过在 `webpack.config.js` 中配置 `entry` 属性，来指定一个（或多个）不同的入口起占

### 单入口

```js
//处理当前文件目录
const path = require('path');
module.exports={
    //入口文件配置项
    entry:{
        main:''
    },
    //出口文件配置项
    output:{
        path:path.resolve(__dirname,''),
        filename:''
    }
}
```

### 多入口

```js
//处理当前文件目录
const path = require('path');
module.exports={
    //入口文件配置项
    entry:{
        main:'....main.js',
        index:'....index.js'
    },
    //出口文件配置项
    output:{
        path:path.resolve(__dirname,'输出文件位置'),
        filename:'[name].js'
    }
}
```

## 模块

模块主要是运用各种loader 用于对模块的源代码进行转换，将 lass\sass 或者 es6\TSfii% 转换为 html 能识别的 css,js 等等，或者进行一些代码压缩图片压缩等等得处理style-loader:处理 css 文件中的 ur | 0 等