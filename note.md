* [free_course](#免费课程笔记)
* [chrome调试](#chrome调试)

### 免费课程笔记
```bazaar
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

```bazaar
command option j 打开chrome console
左上角清理日志
获取元素数值
    > app.$data.inputValue 回车 看双向绑定

```

- 指令
```bazaar
循环
<li v-for="item in list">{{item}}</li>

方法绑定
<button v-on:click="handleBtnClick">提交</button>

双向绑定
<input type="text" v-model="inputValue"/>

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
    