<template>
  <div id="app">
    <input type="text" v-model="newItem" @keyup.enter="addNewItem" placeholder="输入任意键后点击enter">
    <h1>this is a msg from {{sonMsg}}</h1>
    <h2>{{newMsg}}</h2>
    <ul>
      <li v-for="item in items" :class="{best : item.isFinished}" @click="changeStatus(item)">
        {{ item.label }}
      </li>
    </ul>
    <app-son sayhello="Have fun in Vue studying!" :title="title" 
    @listenSth="toDoMsg"></app-son>
  </div>
</template>

<script>
import Store from "./store";
import AppSon from "./components/AppSon"

export default {
  name: 'App',
  data () {
    return {
      title: 'test data',
      items: Store.fetch(),
      newItem: '',
      sonMsg: '',
      newMsg: ''
    }
  },
  components: {
    AppSon
  },
  methods: {
    changeStatus (item) {
      item.isFinished = !item.isFinished;
    },

    addNewItem () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      });
      this.newItem = '';
    },

    toDoMsg (msg) {
      this.sonMsg = msg;
    },


  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items);
      },
      deep: true
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
input {
  margin-left: 1.5rem;
}
li {
  display: block;
  text-align: center;
  list-style-type:none;
  color:#fff;
  width:10rem;
  padding:1rem;
  margin:0 auto 1rem;
  font-size: 1rem;
  border-radius:3px;
  background-color: green;
}
li.best {
  background-color: red;
}
h1, h2 {
  font-weight: normal;
  color: #42b983;
}
</style>
