# demo01

梦诚科技第一次作业


## VUE框架

### 1、vue框架

**原生JavaScript实现的一个遍历数据显示的实例**

```html
<body>
  
    <ul id='list'></ul>
    <script type="text/javascript">
        let person = [
            {id:'001', name:'张三',age:18},
            {id:'002', name:'李四',age:19},
            {id:'003', name:'王五',age:20}
    ]
    let htmlStr = ''
    person.forEach( p=>{
        htmlStr += `<li>${p.id}-${p.name}-${p.age}</li>`
    });
    let list=document.getElementById('list')
    list.innerHTML = htmlStr
    </script>  
</body>
```

**用Vue如何解决**

这里先看个小案例

```html
<body>
    <!-- 
	-->
    <div id="root">
        <h1>你好，{{name}}{{age}}</h1>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false//阻止Vue在启动时产生生产提示
        //创建Vue实例
        new Vue({
            el:'#root',//el用于指定当前Vue实例为哪个容器服务，但通常为css选择器字符串
            data:{//data中用于存储数据，数据供el所指定的容器去使用，但我们暂时先写一个对象
                name:'张重恩',
                age:'233'
            }
        })


    </script>
</body>
```

**注意：** `<font color='red' size='3.5'>`Vue实例和容器必须一一对应 `</font>`

1、想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象

2、root容器里面的代码依然符合html规范，只不过混入了一些特殊的Vue语法

3、root容器里面的代码被称为**Vue模板**

4、Vue实例和容器是一一对应的

5、真实开发中只有一个Vue实例，并且会配合着组件一起使用

6、{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性

7、一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新

- Vue插值语法
  1、功能：用于解析标签体内容
  2、{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性

  ```html
  <body>
      <div id="root">
          <h1>
              你好，{{name}}
          </h1>
          <hr/>
      </div>

      <script>
      	new Vue({
              el:'#root',
              data:{
                  name:'插值语法'
              }
          })
      </script>
  </body>
  ```
- 指令语法
  1、功能：用于解析标签（包括：标签属性，标签体内容，绑定事件......）
  2、用法和简写：v-bind:href="xxx"或简写成:href="xxx"，xxx同样要写成js表达式，且可以直接读取到data中的所有属性

  ```html
  <body>
      <!--  -->
      <div id="root">
          <h1>1、{{name1}}</h1>
          <hr>
          <h1>1、{{name2}}</h1>
          <a :href=url1>点我进入时光荒凉了来时路的博客主页</a>
          <!-- 指令语法的两种方式 v-bind:会将标签体里的内容当表达式进行解析，否则标签体的内容就是字符串，而v-bind:的简写就是: -->
          <a v-bind:href=url2>点我百度</a>
          <hr>
      </div>
      <script type="text/javascript">
          Vue.config.productionTip = false//阻止Vue在启动时产生生产提示
          //创建Vue实例
          new Vue({
              el:'#root',
              data:{
                  name1:'插值语法',
                  name2:"指令语法",
                  url1:"http://blog.zhangchongen.cn/",
                  url2:"https://www.baidu.com/"
              }
          })
      </script>
  </body>
  ```
- 多级结构
  仍然看上面的代码示例，有name1和name2，我们来通过多级结构进行区分

```html
<body>
    <!--  -->
    <div id="root">
        <h1>1、{{name}}</h1>
        <hr>
        <h1>1、{{school.name}}</h1>
        <a :href=url1>点我进入时光荒凉了来时路的博客主页</a>
        <!-- 指令语法的两种方式 v-bind:会将标签体里的内容当表达式进行解析，否则标签体的内容就是字符串，而v-bind:的简写就是: -->
        <a v-bind:href=url2>点我百度</a>
        <hr>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false//阻止Vue在启动时产生生产提示
        //创建Vue实例
        new Vue({
            el:'#root',
            data:{
                name:'插值语法',
                school:{//使用多级结构解决重名问题
                    name:"指令语法",
                    url1:"http://blog.zhangchongen.cn/",
                    url2:"https://www.baidu.com/"
                }
            
            }
        })
    </script>
</body>
```

- 数据绑定
  1、单向数据绑定(v-bind)：数据只能从data流向页面
  2、双向数据绑定(v-model)：数据双向流动
  3、注意：双向绑定一般都应用在表单类元素上（例如：input，select等）

4、v-model:value可以简写成v-model，因为v-model默认手机的就是value值

```html
<body>
    <div id="root">
        单向数据绑定：<input type="text" v-bind:value="name"><br>
        双向数据绑定：<input type="text" v-model:value="name"><br>
        <!-- v-bind：的简写 -->
        单向数据绑定：<input type="text" :value="name"><br>
        <!-- v-model:的简写 -->
        双向数据绑定：<input type="text" v-model ="name"><br>
    </div>
    <script>
        new Vue({
            el:"#root",
            data:{
                name:"张重恩"
            }
        })
    </script>
</body>
```

- **el和data的两种写法**
  **el两种写法：**

  ```javascript
  new Vue({
      el:'#root',//第一种绑定容器的方法
      data:{

      }
  })
  const v = new Vue({
      data:{

      }
  }) 
  //mount:”挂载“的意思，意味着将容器挂载在这个Vue实例上
  v.$mount('#root')//第二种绑定容器的写法，可以用于一个定时器，相对来说比较灵活
  ```

  **data两种写法：对象式，函数式**
  后面学习组件时，data必须用函数式，否则会报错

  **重要原则：由Vue管理的函数，一定不要用箭头函数，一旦写了箭头函数，this就不再是Vue的实例了。**

  ```javascript
  new Vue({
      el:'#root',
      data:function(){
          console.log('@@@',this)
          return {
              name:'对象式'
          }
      }
      //或者下面函数写法
      data(){
      	console.log('@@@',this)
          return {
              name:'对象式'
          }
  	}
  })
  ```
-

学习Vue之前需要掌握的JavaScript基础知识有这些：

- ES6语法规范
- ES6模块化
- 包管理器
- 原型，原型链
- 数组常用方法
- axios
- promise

### 2、vue-cli

### 3、vue-router

### 4、vuex

### 5、element-ui

### 6、vue3
