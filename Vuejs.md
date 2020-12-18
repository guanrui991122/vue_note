# 1.认识Vue.js

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。

```
1.渐进式意味着可以将Vue作为英勇的一部分嵌入其中，带来更丰富的交互体验。
2.将更多的业务逻辑使用Vue实现，Vue的核心库以及其生态系统，如：Core + Vue-router + Vuex，可以满足各种需求
```

Vue的特点和Web开发中常见的高级功能

- 解耦视图和数据
- 可复用的组件
- 前端路由技术
- 状态管理
- 虚拟DOM

# 2.Vue.js安装

**方式一：直接CDN引入**

```html
<! --开发环境版本，包含了有帮助的命令行警告-->
<script src="https ://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!--生产环境版本，优化了尺寸和速度-->
<script src="https : / / cdn.jsdelivr.net/npm/vue"></script>
```



**方式二：下载和引入**

```html
开发环境
https :/ /vuejs.org/js/vue.js
生产环境
https: / /vuejs.orgljs/vue.min.js
```



**方式三：NPM安装**

```
npm install vue
```

# 3.Vue案例

## 第一个案例   <u>初步了解Vue</u>

![image-20201216143616131](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216143616131.png)

```
1.el 属性:该属性决定了这个Vue对象挂载到哪一个元素，此时为挂载到id为app的元素上
2.data属性：该属性通常会存储一些数据
	数据可以直接定义，如上图;
	也可以来自网络，从服务器加载，如下图
```

![image-20201216144129984](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216144129984.png)



## 第二个案例    <u>列表展示</u>

![image-20201216150538037](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216150538037.png)

```
使用v-for指令，对数组movies进行遍历，这种操作属于响应式，即：当数组中的数据发生改变时，界面会自动随之改变，如下图
```

![image-20201216150856255](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216150856255.png)

## 第三个案例      <u>计数器</u>

![image-20201216153111315](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216153111315.png)

```
使用v-on指令进行监听，指定监听事件，再指定监听效果
```

![image-20201216154922786](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216154922786.png)

```
1.methods 属性：用于在Vue对象中定义方法
2.@click 指令：用于监听某个元素的点击事件，并且需要指定当发生点击时，执行的方法（方法通常是methods中定义的方法），
@click可与v-on:click互换
```

# 4.Vue中的MVVM

## 定义

**MVVM**（**Model–view–viewmodel**）是一种软件[架构模式](https://bk.tw.lvfukeji.com/baike-架构模式)。

```
View层:视图层
在我们前端开发中，通常就是DOM层。主要的作用是给用户展示各种信息。
Model层:数据层
数据可能是我们固定的死数据,更多的是来自我们服务器，从网络上请求下来的数据。
在我们计数器的案例中，就是后面抽取出来的obj，见下下图当然，里面的数据可能没有这么简单。
vueModel层:视图模型层
视图模型层是view和Model沟通的桥梁。
一方面它实现了Data Binding，也就是数据绑定，将Model的改变实时的反应到view中;
另一方面它实现了DOM Listener，也就是DOM监听，当DOM发生一些事件(点击、滚动、touch等)时，可以监听到，并在需要的情况下改变对应的Data。

```

![image-20201216162729982](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216162729982.png)

![image-20201216163317845](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201216163317845.png)

# 5.创建Vue实例传入的options

详细解析：https://cn.vuejs.org/v2/api/

##### 目前掌握选项

```
1.el:
	类型：Object |HTMLElement
	如：el:document.querySelector()
	作用：决定之后Vue实例会管理哪一个DOM。
	
2.data：
	类型：Object | Function(组件当中data必须是一个函数)
	作用：Vue实例对应的数据对象。
	
3.methods：
	类型：{ [key: string]: Function }
	作用：定义属于Vue的一些方法，可以在其他地方使用，也可以在指令中使用。
```



# 6.Vue的生命周期

### Vue的生命周期函数

```
1.beroreCreate
2.created
3.beroreMount
4.mounted
5.beforeDestroy
6.destroyed
7.updated
8.beforeUpdate
```



# 7.模板语法

## 模板语法的简单运用

![image-20201217090901814](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217090901814.png)

![image-20201217091001127](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217091001127.png)



# 8.v-xxx 指令

### 1.v-once

```
1.该指令后面不需要跟任何表达式（与v-for不同）
2.该指令表示元素和组件只渲染一次，不会随着数据的改变而改变
指令效果如下图
```

![image-20201217091359376](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217091359376.png)

![image-20201217091428867](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217091428867.png)

### 2.v-html

```
1.当从服务器请求到的数据本身就是一个HTML代码，可以使用v-html
2.该指令后面往往会跟上一个string类型
3.会将string的html解析出来并且进行渲染
指令效果如下图
```

![image-20201217092501703](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217092501703.png)

![image-20201217092537642](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217092537642.png)

### 3.v-text

```
1.v-text作用和Mustache比较相似：都是将数据显示在页面中
2.v-text通常情况下，接受一个string类型
3.使用起来不太灵活（无法在前后添加其他单词），运用较少
```

![image-20201217093337681](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217093337681.png)

![image-20201217094117935](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217094117935.png)

### 4.v-pre

```
1.用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法
2.根据下图可看出该指令的效果
```

![image-20201217200517748](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217200517748.png)

![image-20201217094258934](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217094258934.png)

### 5.v-cloak

```
在某些情况下，例如网络延迟，浏览器可能会直接显示出未编译的mustache标签，使用v-cloak可以避免这种情况。
如下图，使用setTimeout模拟延时显示，页面显示会跟随延时操作同步显示，避免出现为编译标签。
```

![image-20201217105620360](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217105620360.png)

### 6.v-bind

##### 简单运用

```
1.作用：动态绑定属性
2.缩写：：
3.预期：预期:any (with argument) | Object (without argument)
4.参数:attrOrProp (optional)
```

![image-20201217141417718](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217141417718.png)

**简写方式：**

![image-20201217141539849](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217141539849.png)

#### 1.绑定class

##### 1.对象语法

```
用法一：直接通过{}绑定一个类
<h2 :class="{'active':isActive}">{{message}}</h2>

用法二：通过判断，传入多个值
<h2 v-bind:class="{类名1:Boolean, 类名2:Boolean}">{{message}}</h2>

用法三：和普通的来同时存在，并不冲突
<h2 class="类名" v-bind:class="{类名1:Boolean, 类名2:Boolean}">{{message}}</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">{{message}}</h2>
```

![image-20201217150011093](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217150011093.png)



##### 3.数组语法

![image-20201217160822382](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217160822382.png)

#### 2.绑定style

##### 1.对象语法

```
1.对象的key是CSS属性名称
2.对象的value是具体赋的值，只可以来自于data中的属性
```

```
<h2 :style="{key(属性名):value(属性值)}">{{message}}</h2>
```



##### 2.数组语法

```
多个值以,分割
```

![image-20201217181658337](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217181658337.png)

# 9.计算属性

#### 1.基本使用

![image-20201217193317048](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201217193317048.png)

#### 2.复杂操作

![image-20201218091654587](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218091654587.png)

#### 3.setter和getter

![image-20201218091748252](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218091748252.png)

#### 4.计算属性和methods的对比

##### 计算属性优点

```
计算属性会进行缓存，如果多次使用时，计算属性只会调用一次
```

代码截图：

![image-20201218092208993](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218092208993.png)

运行结果展示：

![image-20201218092721646](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218092721646.png)

# 10.ES6部分语法

## 1.块级作用域（let和var的区别）

```
1.变量作用域：变量在什么范围内是可用的
2.ES5中的var是没有会计作用域的
3.ES6中的let是由块级作用域的（if/for）
```

## 2.const关键字

``` 
1.使用const修饰的标识符为常量，不可以再次被赋值
2.在ES6开发中，优先使用const，只有需要改变某一个标识符的时候才使用let
注意：1.使用const修饰的标识符必须被赋值
	 2.常量的含义是指向的对象不能修改，但是可以改变对象内部的属性
```

![image-20201218103523809](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218103523809.png)

## 3.对象的增强写法

<img src="C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218111933532.png" alt="image-20201218111933532" style="zoom:80%;" />

<img src="C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218111950317.png" alt="image-20201218111950317" style="zoom:80%;" />



# 11.事件监听

### 1.v-on的基本使用

```
1.作用：绑定事件监听器
2.缩写：@
3.参数：event
4.预期：Function | Inline Statement | Object
```



![image-20201218114824425](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218114824425.png)



### 2.参数问题

```
1.事件调用的方法没有参数
	可以忽略小括号


```



<img src="C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20201218152704254.png" alt="image-20201218152704254" style="zoom: 200%;" />

































































