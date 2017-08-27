# todolist

> 使用Vue.js实现一个todolist，使用localStorage存储，即使网页刷新，数据依然不变

![todolist演示](https://raw.githubusercontent.com/zyucong/MarkdownPhoto/master/2017/August/todolist.gif)

## Development

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev
```

## Introduction
App.vue文件注册了组件todo-component，主要布局都在组件todo-component
```js
import todoComponent from './components/todo-component'
export default {
  components: { todoComponent },
}
```
`<template>`标签内的网页结构如下，其中输入框用v-model绑定数据，监听到回车键按下之后执行新增todolist函数<br>
`<li>`内注册DOM事件监听光标移入移出，改变Delete所在span的v-show。监听光标点击事件，改变finished的显示。用v-for遍历todolist里面存储的条目，根据index动态改变条目的序号。
```html
  <div class="app" >
    <h1 class="title">{{title}}</h1>
    <input v-model="newtodo" @keyup.enter="addNew" placeholder="do what"
    class="app-input">
    <ul class="ulist">
      <li
      v-for = "(item, index) in todolist"
      @mouseenter="showDelete(item)"
      @mouseleave="hideDelete(item)"
      ><h3>
      <!--<input type="checkbox"
      :checked="item.isfinished"
       @click = "toggleFinish(item)">-->
      <span class="item-label" :class="{finished: item.isfinished}"
      @click = "toggleFinish(item)">
        {{ index + 1 }} . {{ item.text }}</span>
      <span class="status" v-show="item.isfinished">finished</span>
      <span class="item-delete" v-show="item.candelete"
      @click="deleteClick(index)">Delete</span>
      </h3>
    </li>
  </ul>
  </div>
```
`<sript>`标签内的js代码如下。data中声明的变量newtodo用于新增todo，todolist的数据通过访问localStorage获取得到一个数组。按下回车后除将`<input>`中的内容增加至todolist数组末尾外，
还有两个不会显示的数据isfinished和candelte，初始值都是false，监听到相应事件会改变这两个值，改变finished和delete的显示。删除操作通过数组的原型方法splice()实现。
watch对象在todolist发生变化后将数据保存到localStorage中。
```js
import Store from '../store'
export default {
  name:"",
  data(){
    return{
      title:"todo-vuejs",
      newtodo:'',
      todolist:Store.fetch(),
    }
  },
  methods:{
    toggleFinish: function(item){
      item.isfinished = !item.isfinished
    },
    showDelete: function(item){
      item.candelete = true
    },
    hideDelete: function(item){
      item.candelete = false
    },
    addNew: function(newtodo){
      this.todolist.push({
        text:this.newtodo,
        isfinished:false,
        candelete:false
      })
      this.newtodo = ''
    },
    deleteClick: function(index){
      this.todolist.splice(index,1)
    }
  },
  watch:{
    todolist: {
      handler:function(val){
        Store.save(val) },
      deep: true
    }
  }
}
```
store.js文件定义的fetch()和save()方法，通过JSON处理存储和获取得到的数据。
```js
const STORAGE_KEY = 'todos-vuejs'
export default {
  fetch: function() {
    return JSON.parse(window.localStorage.getItem(STORAGE_KEY) || '[]')
  },
  save: function(items){
    window.localStorage.setItem(STORAGE_KEY, JSON.stringify(items))
  }
}
```

