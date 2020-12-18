## 模块原理

> - 在Node中，每个模块内部都有一个自己的module对象
>
> - 该module对象中，有一个成员叫：exports也是一个对象
>
> - 默认在代码的最后有一句：return module exports
>
> - 最后return的是module .exports，不是exports
>
> - module .exports === exports
>
>   ``` 
>   一旦使用exports = {}，则断开module .exports和exports的联系，之后再也无法通过使用exports .变量名来对module .exports .变量名进行操作
>   ```
>
> - 使用方法：
>
>   ###### 导出单个成员
>
>   - module .exports
>
>   ###### 导出多个成员
>
>   - 方法一：exports .xx= xx
>   - 方法二：module .exports = {}
>
> - 而`exports`只是`module.exports`的一个引用
>   所以即便你为`exports = xx`重新赋值，也不会影响`module.exports`
>   但是有一种赋值方式比较特殊:`exports = module.exports`这个用来重新建立引用关系的

# const

定义：用来定义常量，一旦被定义后，就不可修改

## require标识符分析

- 核心模块的本质也是文件
- 第三方文件
  - 凡是第三方模块都必须通过npm下载
  - 不可能有任何一个第三方包和核心模块的名字是一样的
  - 既不是核心模块，也不是路径形式的模块
  - 如果package.json文件不存在或者main指定的入口模块也没有，则node会自动找该目录下的index.js，也就是说index.js会作为一个默认备选项，如果以上任何条件都不成立，则会进入上一级目录中查找，如果没有，则一直继续往上一级查找，直到当前磁盘根目录还找不到，最后报错：can not findmodule xxx



# 模块加载机制

- 优先从缓存加载

- 核心模块

- 路径形式的文件模块

- 第三方模块

  ![image-20201123102438347](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201123102438347.png)

- 一个项目有且仅有一个node_modules 而且是存放到项目的根目录

  

## npm

node package manager

#### npm网站

npmjs.com

#### npm命令行工具

npm 的第二层含义就是一个命令行工具，只要你安装了node就已经安装了npm。

npm也有版本这个概念。

可以通过在命令行中输入:

``` shell
npm --version
```

升级npm(自己升级自己):

``` shell
npm install --global npm
```

#### 常用命令

- npm init
  - npm init -y 可以跳过向导，快速生成   //自己就不能去修改信息了
- npm install
- npm install 包名
  - 只下载
- npm install --save 包名
  - 下载并且保存依赖项（package.json文件中的dependencies选项）
  - npm i -S 包名

- npm uninstall  包名
  - 只删除，如果有依赖项会依然保存
  - npm un 包名
- npm uninstall --save 包名
  - 删除的同时也会把依赖信息也去除
  - npm un -S 包名

- npm help
  - 查看使用帮助
- npm 命令 -- help
  - 查看指定命令的使用帮助

#### 解决npm被墙问题

npm存储包在国外，有时候会被墙，速度很慢

淘宝国内的npm备份：https://npm.taobao.org/

- 安装淘宝的cnpm：

  ``` javascript
  #在任意目录执行都可以
  #--global表示安装到全局,而非当前目录
  npm install -global cnpm 
  ```

  

  安装包的时候把之前的 `npm` 替换成 `cnpm` 。

- 不想安装，想直接使用，则：

  ``` 
  npm install -g cnpm --registry=https://registry.npm.taobao.org
  ```

  可以直接将这个选项加入配置文件中



## package.json

- 每一个项目都要有一个`package.json`文件（包括描述文件，即产品的说明书）
- 这个文件可以通过`npm init` 的方式进行自动初始化出来

``` 
name : (npm-demo)    //括号内为默认文件名，可以在后面写自己想起的名字
version: (1.0.0)0.0.1   //此为最低版本号，后面升级，则可更改新的版本号
description:这是一个测试项目  //描述
entry point: (index.js) main.js   //指定接口
test command :
git repository :
keywords:
author: lipengzhou  //编写文件的作者
license: (ISC)
```

对于咱们目前来讲，最有用的是那个`dependencies`选项，可以用来帮我们保存第三方包的依赖信息。

如果你的`node_modules`删除了也不用担心，我们只需要: `npm install`就会自动把`package.json`中的`dependencies`中所有的依赖项都下载回来。|

- 建议每个项目的根目录下都有一个 `package.json`文件
- 建议执行`npm install`包名的的时候都加上 `--save`这个选项，目的是用来保存依赖项信息

# Express

引包

```javascript
var express = require('express')
```

创建服务器应用程序,即原来的http.creatServer

```javascript
var app = express()
```

当服务器收到get请求 /的时候，执行回调处理函数

```javascript
app.get('/',function(request,response){  //get的第一个参数是url地址
    response.send('hello express!')
})
```

公开指定目录

只要这样做了，你就可以直接通过/public/xx的方式访问 public目录中的所有资源

```javas
app.use('/public/',express.static('./public/'))
//第一个参数为url地址，第二个参数为被公开的文件的目录
```

#### .1起步

```shell
npm install --save express
```



### .1.4基本路由

##### get：

``` javascript
//当你以,GET方法请求/的时候,执行对应的处理函数
app.get('/', function (req，res){
    res.send( 'Hello wor1d!')
})
```

##### post:

``` javascript
//当你以POST方法请求/的时候,指定对应的处理函数
app.post( '/',function(req,res){
    res.send( "Got a PoST request")
})

```

### 静态服务

``` javascript
// /public资源
app.use(express.static('public')
        
// /files资源
app.use(express.static('files')

// /public/xxx
app.use('/public', express.static('public'))

// /static/xxx
app.use( "/static", express.static('public')
        
app.use( " /statie" , expeS3.static(path.join(__dirname，'public')))

```

### .2在Express中配置使用  `art-template`  模板引擎

- [art-template官方文档](https://aui.github.io/art-template/)

- 安装

  ```she
  npm install --save art-template
  npm install --save express-art-template
  ```

- 配置

  配置使用art-template模板引擎

  - 第一个参数表示，当渲染以  `.art`  结尾的文件的时候，使用 art-template 模板引擎
  - express-art-template 是专门用来在Express 中把 art-template 整合到 Express 中
  - 因为 express-art-template 依赖了 art-template，虽然外面这里不需要记载art-template但是也必须安装

  ```javascript
  app.engine('art', require('express-art-template'))
  ```

- 使用 

  - Express 为 Response 相应对象提供了一个方法 : render
  - render方法默认是不可以使用，但是如果配置了模板引擎就可以使用了res.render( 'html模板名',{模板数据)}
    - 第一个参数不能写路径，默认会去项目中的 views目录查找该模板文件,也就是说 Express有一个约定:开发人员把所有的视图文件都放到views目录中

  ``` javascript
  app.get('/', function (req,res){
  res.render('404.htm1')
  })
  ```

- 如果想要修改默认的 `views` 视图渲染存储目录，则可以

  ``` javas
  app.set( 'views',render函数的默认路径)      //views是一个特定指定的固定字符，千万不能写错
  ```

### .3在Express中获取表单GET请求参数

Express内置了一个api，可以直接通过`req.query`来获取数据

``` javascript
// 通过requery方法获取用户输入的数据
// req.query只能拿到get请求的数据
 var comment = req.query;
```

### .4在Express获取表单POST请求体数据

在Express，使用  `body-parse`

安装：

```shell
npm install --save body-parser
```

配置：

```javascript
var express = require('express')
// 引包
var bodyParser = require('body-parser')

var app = express()

// 配置body-parser
// 只要加入这个配置，则在req请求对象上会多出来一个属性：body
// 也就是说可以直接通过req.body来获取表单post请求数据
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))

// parse application/json
app.use(bodyParser.json())
```

使用：

``` javascript
app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  // 可以通过req.body来获取表单请求数据
  res.end(JSON.stringify(req.body, null, 2))
})
```

## 模块分类

### 模块职责要单一，不要乱写

划分模块的目的就是为了增强项目的可维护性，提升开发效率

#### app.js 入门模块

职责：

``` 
创建服务
做一些服务相关的配置
	模板引擎
	body-parse 解析表单post请求体
	提供静态资源服务
挂载路由
监听端口启动服务
```

#### router.js 路由模块

职责：

``` 
处理路由
根据不同的请求方法 + 请求路径设置具体的请求处理函数
```

#### student.js 数据操作文件模块

职责：

``` 
操作文件中的数据，只处理数据，不关心业务
```



# 其它

- 配置模板引擎和body-parse 一定要在app.use（router）前面

- 如果需要获取一个函数中异步操作的结果，则必须通过回调函数来获取

#### - 模块标识

- 文件操作中的相对路径可以省略 ./

  模块加载中，相对路径中的./不能省略

- 所有文件操作的API都是异步的
- require（'文件路径'）  //不能省略   `.`   ，否则会在磁盘根目录进行寻找

# MongoDB

