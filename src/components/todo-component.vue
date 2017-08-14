<template lang="html">
  <div class="app" >
    <h1>{{title}}</h1>
    <input v-model="newtodo" @keyup.enter="addNew" placeholder="do what"
    class="app-input">
    <ul>
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
      <span class="status" v-if="item.isfinished">finished</span>
      <span class="item-delete" v-if="item.candelete"
      @click="deleteClick(index)">Delete</span>
      </h3>
    </li>
  </ul>

  </div>
</template>

<script>
import Store from '../store'
//console.log(Store)
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
      handler:function(val){ Store.save(val) },
      deep: true
    }

  }
}
</script>

<style lang="css">
.app{
  width: 800px;
  margin: 30px auto;
}
.app-input{
  width: 750px;
  height: 35px;
  padding: 0 5px;
}
.finished{
  text-decoration: line-through;
}
.status{
  background: red;
  color: white;
  padding: 0 5px;
  font-size: 12px;
}
.item-delete{
  text-decoration: underline;
  cursor: pointer;
  font-size: 12px;
  color: grey;
}
</style>
