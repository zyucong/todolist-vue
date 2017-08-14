<template>
  <div class="hello">
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
  </div>
</template>

<script>
new Vue({
  el: '#app',
  data:{
    todolist:[
      {
        text:'买菜',
        isfinished: false
      },
      {
        text: '做饭',
        isfinished: true
      }
    ],
    newtodo: ''
  },
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
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished{
  text-decoration: line-through;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
