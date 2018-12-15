<template>
<div class="hello">
  <h1>{{msg}}</h1>
  <h1>{{msgFromFather}}</h1>
  <button @click="onClickMe">open mouth!</button>
</div>
</template>

<script>
export default {
  name: 'componentA',
  data () {
    return {
      msg: 'hello from component A'
    }
  },
  props: ['msgFromFather'],
  // events: {
  //   'onAddNew': function (items) {
  //     console.log(items)
  //   }
  // },
  methods: {
    onClickMe: function () {
      // console.log(this.msgFromFather)
      this.$emit('child-tell-me-something', this.msg)
      // this.$dispatch('child-tell-me-something', this.msg) //1.x中的方法，已被废弃
    }
  }
}
</script>
<style scoped>
h1{
  color: #42b983
}
</style>
