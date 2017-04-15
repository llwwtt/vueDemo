<template>
  <div id="app">
    <h1>{{title}}</h1>
    <input v-model="newItem" @keyup.enter="addNew()">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" @click='toggleFinish(item)'>
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
  import Store from './store'
  // console.log( Store.fetch(items))
 
  export default {
    data: function () {
      return {
        title: 'this is a todo list',
        items: Store.fetch(),
        newItem: ''
      }

    },
    watch: {
      //每一次新增items时，都会执行一遍handler中的语句
      items: {
          handler: function(items){
            Store.save(items)
        },
      deep:true
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
        });
        this.newItem = '';
      }
    }
  }

</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  .finished {
    text-decoration: line-through red;
  }

</style>
