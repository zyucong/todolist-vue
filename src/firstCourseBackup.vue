<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <!--<hello></hello>-->
    <input v-model="newtodo" @keyup.enter="addNew">
    <ul>
      <li
      v-for="item in todolist"
      :class="{finished: item.isfinished}"
      @click="toggleFinish(item)"
      >
      {{ item.text }}
    </li>
    </ul>
    {{newtodo}}
    <componentA
    msgFromDaddy="yeah"></componentA>
  </div>
</template>

<script>
import Store from './store'
//console.log(Store)
import componentA from './components/componentA'
export default {
  //name: 'app',
  data: function(){
    return  {
      todolist:Store.fetch(),
      newtodo: ''
    }
  },
  components: { componentA },
    methods:{
      toggleFinish: function(item){
        item.isfinished = !item.isfinished
      },
      addNew: function(newtodo){
        this.todolist.push({
          text: this.newtodo,
          isfinished: false
        })
        this.newtodo = ''
      }
    },
    watch:{
      todolist:{
        handler: function(val){
            Store.save(val)
        },
        deep: true
      }
    }
}
</script>

<style>
.finished{
  text-decoration: line-through;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
