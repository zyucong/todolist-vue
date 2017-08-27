<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <!--<hello></hello>-->
<todo-component></todo-component>
  </div>
</template>

<script>
//import Store from './store'
//console.log(Store)
import todoComponent from './components/todo-component'
export default {
  //name: 'app',
  data: function(){
    return  {
    }
  },
  components: { todoComponent },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
