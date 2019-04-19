* [free_course](#免费课程笔记)
* [chrome调试](#chrome调试)
* [vue指令](#vue基本指令)
* [组件化](#组件化)
* [Vue实例](#Vue实例)
* [模板语法](#模板语法)
* [计算,方法,监听器](#计算,方法,监听器)
* [Vue中的样式绑定](#Vue中的样式绑定)
* [数组与对象set](#数组与对象set)
* [vue指令](#vue指令)


### 免费课程笔记
```
index.html
    挂载点，模板，实例之间的关系
index2.html
    属性绑定和双向绑定
index3.html
    计算属性与监听器
index4.html
    v-if,v-show,v-for 指令
index5.html
    TodoList
index6.html
    TodoList 组件拆分
index7.html
    TodoList 删除功能

大型项目使用webpack打包:
    Vue-cli脚手架工具,快速构建标注vue项目,迅速上手工程级别vue项目开发
    npm install --global vue-cli
    vue init webpack Vue_introduction
```

### chrome调试

```
command option j 打开chrome console
左上角清理日志
获取元素数值
    > app.$data.inputValue 回车 看双向绑定

```

### vue基本指令
- 循环
```
<li v-for="(item,index) in list">{{item}}</li>

循环建议使用key值,但不建议:key="index" 
建议用数据库id作为key
  <div v-for="(item, index) of list"
             :key="item.id">
            {{item.text}} --- {{index}}
        </div>
   data: {
                   list: [{
                       id: "1234555",
                       text: "hello"]
                   }

对对象的循环遍历
 <div v-for="(item,key,index) of userInfo">
                        
                    
```
```
方法绑定
<button v-on:click="handleBtnClick">提交</button>

双向绑定
<input type="text" v-model="inputValue"/>

--v-show与v-if关系
v-show=false div标签被 display=none 性能高
v-if=false div标签在页面删除

--if与else要紧贴着使用
<div v-if="show">
            {{message}}
        </div>
<div v-else>
            bye
        </div>

--必须加上key,否则input会被复用        
<div v-if="show">
    用户名: <input key="username" />
</div>
<div v-else>
    邮箱名: <input key="email" />
</div>
                
```
- MVP传统模式 面向Dom编程
    - Model View Presenter   MVP
    - jquery.html jquery.js
    - V: 视图  
    - P: 控制器 方视图和模型层的中转 大量代码在做DOM操作
    - 视图点击 控制器去执行 调用ajax获取模型层数据 通过DOM改变视图

- MVVM 面向数据编程
    - Model View ViewModel
    - ViewModel无需关注 内置负责联系M与V
    - 只需关注Model与View层
    - Model层 data
    - View层 模板

### 组件化
- 全局组件 
    - Vue.component("TodoItem") 使用时 <todo_item> 约定
    - v-bind:content="item
    - 子组件用props: ['content','index'] 接收外部传值 

- 局部组件
    - var TodoItem ={}
    - 在 new vue中 components: {TodoItem: TodoItem}
    
- 子组件传值
    - <li @click='handleItemClick'>
    - methods:{handleItemClick function(){this.$emit("delete",this.index)} }    

- 父组件监听子组件
    - @delete="handleItemDelete"> 监听子组件删除动作,后调用父组件方法
    - handleItemDelete(index)    

- table中tbody放组件问题
    - 浏览器要求tbody里必须放tr,<table><tbody><tr>,所以放子组件row会有问题
    - 这样解决 <tr is="row"><tr/> 
    - 类似还有<ul><li is="row"> 
    - 类似还有<select><option is="row">

- 子组件中data必须是函数
```
函数方法可以保证data是新对象不共享
data: function () {
                return {
                    content: 'this is a row'
                }
            },
``` 
- 获取Dom内容
    - <div ref="hello">
    - console(this.$refs.hello)
    - console.log(this.$refs.hello.innerHTML)
```
可以用于获取子组件数据,求和
handleChange: function () {
                   this.total = this.$refs.one.number + this.$refs.two.number
                }
```   
- 父组件给子组件传值
```
 父组件
 <counter :count="0"></counter>  //:count 把后面""变成js表达式,变成数值0
 
 子组件用props收
 Vue.component('counter', {
             props: ['count'],
             template: '<div>{{count}}</div>'
         })
 
 父组件给子组件传参,子组件不可修改,单向数据流       
```    
- 组件参数校验
``` 
props: {
                content: {
                    type:  [Number,String],
                    required: true,
                    default: 'default value',
                    validator: function (value) {
                        return (value.length > 5)
                    }
                }
            }       
```
- 父组件监听原生事件,而不是子组件的事件
``` 
 <div id="root">
        <child @click.native="handleClick"></child>
    </div>
```
    
### Vue实例
- app.$el $代码vue的实例方法
- 生命周期钩子函数 
    - 官网Vue实例-生命周期图示 
    - 某些事件点,被自动执行,不定义在methods里
    - beforeCreate: function() {}
    - created: function() {} 
    - beforeMount function() {} 页面渲染前
    - mounted function() {} 页面渲染后    
    - beforeDestroy
    - destroy 
    - beforeUpdate 数据改变,页面重新渲染前
    - updated  数据改变,页面重新渲染后
 
### 模板语法
- {{name}} 插值表达式
- v-text 可以代替插值表达式
- v-html 可以增加<h1>等样式
```
        都可以增加Js表达式
        <div>{{name + ' Lee'}}</div>
        <div v-text="name + ' Lee'"></div>
        <div v-html="name + ' Lee'"></div>
```

### 计算,方法,监听器
- 方法
```
    如果用方法实现fullName,无法被缓存
    methods: {
        fullName: function() {
            return this.firstName+ " "+ this.lastName;
        }
    }
```
- 监听器
```
    firstName lastName不改变,监听也会缓存
    watch: {
        firstName: function() {
            this.fullName = this.firstName + " "+this.lastName;
        }
        lastName: function() {
                    this.fullName = this.firstName + " "+this.lastName;
                }
    }

```
- 计算属性
```
    内置缓存 语法相对于watch更简单 推荐   
    computed: {
                fullName: function () {
                    return this.firstName+ " "+this.lastName;
                }
            }
``` 
### Vue中的样式绑定
- 方式1 class的对象绑定
- style里定义样式
```
   <style>
        .activated {
            color: red
        }
    </style>
```
- div上定义class
```
    <div @click="handleDivClick"
            :class="{activated: isActivated}"
        >Hello world</div>
```
- 控制数据修改dom
```
    handleDivClick: function () {
                    this.isActivated = !this.isActivated
                }
```
- 方式2 数组形式
```
    <div :style="[styleObj,{fontSize: '20px'}]"
            @click="handleDivClick">
                Hello world
            </div>
            
    
     data: {
                    styleObj: {
                        color: "black"
                    }
                },
                methods: {
                    handleDivClick: function () {
                        this.styleObj.color = this.styleObj.color === "black" ? "red" : "black";
                    }
                }
``` 

### 数组与对象set
- 数组增加内容
    - 不能通过数组下标赋值增加数组内容
    - 用vm.list.push({id:001,text:"1"})
    - 数组下标修改无法影响页面
    - push pop shifft(删除第一项) unshift splice sort reverse

- 数组修改内容
    - 不能通过数组下标赋值修改数组内容
    - 用vm.list.splice(1,1, {id:"333", text: "Dell"}) 从下标1删除1条,并增加一条
    - 也可以 vm.$set(vm.userInfo,1,5) 把下标为1的数字改成5
  
- template模板占位符
    - 可以包裹元素进行v-for循环,不会出现在页面上,避免用一个<div>包裹     

- 给对象增加字段
    - Vue.set(vm.userInfo,"address","beijing")
    - vm.$set(vm.userInfo,"address","beijing")     