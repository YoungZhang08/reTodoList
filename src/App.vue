<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-on:keyup.enter="addList" v-model="newList">
    <div class="todolist">
      <ul>
        <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="todoThis(item)">{{item.label}}</li>
      </ul>
    </div>
    <Hello></Hello>
  </div>
</template>

<script>
import Hello from './components/hello.vue';
import Store from './store.js';
export default {
  name: 'app',
  components:{
    Hello
  },
  data () {
    return {
      title:' Youngzhang want to do!',
      items:Store.fetch(),
      newList:''
    }
  },
  watch:{
    items:{
      handler(items){
        Store.save(items);
      },
      deep:true
    }
  },
  methods:{
    todoThis(item){
      item.isFinished = !item.isFinished;
    },
    addList(item){
      this.items.push({
        label:this.newList,
        isFinished:false  
      });
      this.newList = '';
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
.todolist{
  margin: 0 auto;
  width: 400px;
  height: 100%;
}
.todolist ul{
  text-align: left;
}
input{
  width: 350px;
  height: 20px;
}
.finished{
  text-decoration: line-through;
}
</style>
