<template>
  <div class="">
    <h1>{{ msg }}</h1>
    <button @click="onClickMe">Click!</button>
  </div>
</template>

<script>
export default {
  name: '',
  data () {
    return {
      msg: 'hello from component'
    }
  },
  props: ['msgFromDaddy'],
  methods:{
    onClickMe: function(){
      console.log(this.msgFromDaddy)
    }
  }
}
</script>
