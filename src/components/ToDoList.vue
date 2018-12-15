/* eslint-disable */
<template>
  <div class="todo">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew"/>
    <ul>
      <li v-for="item in items" :key="item.id"
          v-bind:class="{finished:item.isFinished}"
          v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <p>child tells me:{{childWords}}</p>
    <ComponentA msgFromFather="msgFromFather"
    v-on:child-tell-me-something="listenToMyBoy"></ComponentA>
    <!--<ComponentA msgFromFather="msgFromFather"></ComponentA>-->
  </div>
</template>

<script>
import Store from '../store'
import ComponentA from './componentA'
export default {
  name: 'ToDoList',
  components: {ComponentA},
  data () {
    return {
      title: 'this is a todo list',
      childWords: '',
      items: Store.fetch(), // [
      // {
      //   label: 'coding',
      //   isFinished: false
      // },
      // {
      //   label: 'reading',
      //   isFinished: false
      // },
      // {
      //   label: 'exercising',
      //   isFinished: false
      // },
      // {
      //   label: 'speaking',
      //   isFinished: true
      // }
      // ]

      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  events: {
    'child-tell-me-something': function (msg) {
      this.childWords = msg
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
      // this.$broadcast('onAddNew', this.items)
    },
    listenToMyBoy: function (msg) {
      this.childWords = msg
    }
  }
}
</script>

<style scoped>
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    /*display: inline-block;*/
    margin: 10px;
  }
  a {
    color: #42b983;
  }
  .finished{
    text-decoration: underline;
  }
</style>
